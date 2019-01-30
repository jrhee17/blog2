---
layout: post
title: 'Mysql Select Flow'
date: '2018-09-03 15:12:11 -0400'
categories: mysql
---

Mysql

- mysql_execute_command
    - Get table to select from
    - Reset connection info
    - Check if read-only query
    - case GTID_STATEMENT_EXECUTE
    - open temporary table
    - case SQLCOM_SELECT
    - check privileges
    - execute_sqlcom_select
        - `open_tables_for_query`
            - `open_tables`
                - for each table do `open_and_process_table`
                    - `open_table`
                        - `open_table_get_mdl_lock`
                            - thd->mdl_context.acquire_lock
                            - ticket
                                ```
                                {
                                ...
                                m_type = MDL_INTENTION_EXCLUSIVE
                                m_duration = MDL_STATEMENT
                                ...
                                }
                                ```
                            - mdl_request
                                ```
                                type = MDL_SHARED_READ
                                duration = MDL_TRANSACTION
                                key = (m_length = 17, m_db_name_length = 7, m_ptr = char [387] @ 0x00007f99fbb1f164)
                                ...
                                ```
                            - try_acquire_lock_impl(mdl_request, &ticket)
                                - check if context already holds shared lock on subject
                                - create MDL_ticket
                                - `MDL_lock::get_unobtrusive_lock_increment`
                                    - `request->key.mdl_namespace()`: TABLE
                                    - `m_object_lock_strategy.m_unobtrusive_lock_increment[request->type]`
                                - `mysql_mdl_create`
                                - `lock= mdl_locks.find_or_insert(m_pins, key, &pinned)`
                                    ```
                                    (MDL_lock) $7 = {
                                      key = (m_length = 17, m_db_name_length = 7, m_ptr = char [387] @ 0x00007fe5f42dc604)
                                      m_rwlock = {
                                        m_prlock = {
                                          lock = (__sig = 1297437786, __opaque = char [56] @ 0x00007fe5f42dc790)
                                          no_active_readers = (__sig = 1129270852, __opaque = char [40] @ 0x00007fe5f42dc7d0)
                                          active_readers = 0
                                          writers_waiting_readers = 0
                                          active_writer = '\0'
                                          writer_thread = 0x0000000000000000
                                        }
                                        m_psi = 0x000000010e4c6100
                                      }
                                      m_granted = {
                                        m_list = {
                                          I_P_List_fast_push_back<MDL_ticket> = {
                                            m_last = 0x0000000103f67200
                                          }
                                          m_first = 0x0000000000000000
                                        }
                                        m_bitmap = 0
                                      }
                                      m_waiting = {
                                        m_list = {
                                          I_P_List_fast_push_back<MDL_ticket> = {
                                            m_last = 0x0000000103f67218
                                          }
                                          m_first = 0x0000000000000000
                                        }
                                        m_bitmap = 0
                                      }
                                      m_hog_lock_count = 0
                                      m_piglet_lock_count = 0
                                      m_current_waiting_incompatible_idx = 0
                                      m_obtrusive_locks_granted_waiting_count = 0
                                      m_fast_path_state = 1048576
                                      m_strategy = 0x0000000101dafbd0
                                    }
                                    ```
                                - check if other locks exist
                                - `lock_object_used`
                                    - If pinned (singleton?), decrement `m_unused_lock_objects`
                                - push to `m_tickets`
                                - `mysql_mdl_set_status(ticket->m_psi, MDL_ticket::GRANTED)`: Set psi status to granted if psi is not null
                            - If ticket is not null, lock was acquired -> return
                        - compute hash
                            ```
                            p table_list->open_strategy
                            (TABLE_LIST::(anonymous enum)) $21 = OPEN_NORMAL
                            ```
                        - Get table cache, lock mutex for table cache, and try to get cached table (if found, unlock mutex)
                        - Add table to `table_list`
                        - Initialize table instance 
                - 'read_lock_type_for_table': Change to TL_READ thread lock (`tbl->reginfo.lock_type`)
        - `handle_query`
            - `select->prepare`: prepare query block for optimization
            - `lock_tables`
                - `mysql_lock_tables`
                    - `lock_tables_check`: check if tables ares locked
                    - `get_lock_data`: create lock
                    - `lock_external`: external ha lock (`F_RDLCK`)
                    - `thr_lock_errno_to_mysql`: lock on half of lock data array
                - `thd->lex->lock_tables_state= Query_tables_list::LTS_LOCKED;`
            - `query_cache.store_query()`
            - `select->join->exec()`: execute query
                - `do_select()`
                    - `first_select`: perform actual query
    - `trans_commit_stmt`: perform transaction commit
    - release metadata locks
