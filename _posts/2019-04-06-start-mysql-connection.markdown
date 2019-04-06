---
layout: post
title: 'Mysql Select Flow'
date: '2018-09-03 15:12:11 -0400'
categories: mysql
---

Mysql

Objective

- Develop a deeper understanding of MySQL internals

```
>Per_thread_connection_handler::add_connection
<Per_thread_connection_handler::add_connection 396
>mysql_socket_vio_new
| >my_raw_malloc
| <my_raw_malloc 219
| >vio_init
| <vio_init 175
<mysql_socket_vio_new 280
>my_hash_init
| >init_dynamic_array
| | >my_raw_malloc
| | <my_raw_malloc 219
| <init_dynamic_array 78
<my_hash_init 120
>my_hash_init
| >init_dynamic_array
| | >my_raw_malloc
| | <my_raw_malloc 219
| <init_dynamic_array 78
<my_hash_init 120
>Security_context::init
<Security_context::init 36
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Ha_trx_info::reset
<Ha_trx_info::reset 94
>Rpl_transaction_ctx::Rpl_transaction_ctx
| >Rpl_transaction_ctx::cleanup
| <Rpl_transaction_ctx::cleanup 40
<Rpl_transaction_ctx::Rpl_transaction_ctx 28
>Rpl_transaction_write_set_ctx::Rpl_transaction_write_set_ctx
<Rpl_transaction_write_set_ctx::Rpl_transaction_write_set_ctx 28
>init_alloc_root
| >my_raw_malloc
| <my_raw_malloc 219
<init_alloc_root 88
>init_alloc_root
<init_alloc_root 88
>init_alloc_root
<init_alloc_root 88
>init_alloc_root
<init_alloc_root 88
>init_alloc_root
<init_alloc_root 88
>init_alloc_root
| >my_raw_malloc
| <my_raw_malloc 219
<init_alloc_root 88
>plugin_thdvar_init
| >plugin_var_memalloc_free
| <plugin_var_memalloc_free 3407
| >intern_plugin_lock
| | >my_raw_malloc
| | <my_raw_malloc 219
| <intern_plugin_lock 840
| >intern_plugin_unlock
| <intern_plugin_unlock 1101
| >intern_plugin_lock
| | >my_raw_malloc
| | <my_raw_malloc 219
| <intern_plugin_lock 840
| >intern_plugin_unlock
| <intern_plugin_unlock 1101
| >my_hash_init
| | >init_dynamic_array
| | | >my_raw_malloc
| | | <my_raw_malloc 219
| | <init_dynamic_array 78
| <my_hash_init 120
| >my_raw_malloc
| <my_raw_malloc 219
| >my_raw_malloc
| <my_raw_malloc 219
| >my_hash_first_from_hash_value
| <my_hash_first_from_hash_value 331
<plugin_thdvar_init 3183
>reset_current_stmt_binlog_format_row
| >set_current_stmt_binlog_format_row
| <set_current_stmt_binlog_format_row 3661
<reset_current_stmt_binlog_format_row 3698
>debug_sync_init_thread
<debug_sync_init_thread 653
>my_hash_init
| >init_dynamic_array
| | >my_raw_malloc
| | <my_raw_malloc 219
| <init_dynamic_array 78
<my_hash_init 120
>my_hash_init
| >init_dynamic_array
| | >my_raw_malloc
| | <my_raw_malloc 219
| <init_dynamic_array 78
<my_hash_init 120
>my_raw_malloc
<my_raw_malloc 219
>my_raw_malloc
<my_raw_malloc 219
>my_hash_first_from_hash_value
<my_hash_first_from_hash_value 331
>my_raw_malloc
<my_raw_malloc 219
>my_hash_first_from_hash_value
<my_hash_first_from_hash_value 331
>my_raw_malloc
<my_raw_malloc 219
>my_hash_first_from_hash_value
<my_hash_first_from_hash_value 331
>my_raw_malloc
<my_raw_malloc 219
>my_hash_first_from_hash_value
<my_hash_first_from_hash_value 331
>my_raw_malloc
<my_raw_malloc 219
>my_hash_first_from_hash_value
<my_hash_first_from_hash_value 331
>my_raw_malloc
<my_raw_malloc 219
>my_free
<my_free 292
>my_hash_free
| >my_free
| <my_free 292
<my_hash_free 185
>my_hash_init
| >init_dynamic_array
| | >my_raw_malloc
| | <my_raw_malloc 219
| <init_dynamic_array 78
<my_hash_init 120
>Gtid::to_string
<Gtid::to_string 195
>my_hash_init
| >init_dynamic_array
| | >my_raw_malloc
| | <my_raw_malloc 219
| <init_dynamic_array 78
<my_hash_init 120
>my_raw_malloc
<my_raw_malloc 219
>my_net_init
| >my_net_set_read_timeout
| | >vio_socket_timeout
| | | >vio_set_blocking
| | | <vio_set_blocking 254
| | <vio_socket_timeout 322
| <my_net_set_read_timeout 1046
| >my_net_set_write_timeout
| | >vio_socket_timeout
| | <vio_socket_timeout 322
| <my_net_set_write_timeout 1057
| >my_raw_malloc
| <my_raw_malloc 219
| >vio_fastsend
| <vio_fastsend 357
<my_net_init 123
>Security_context::set_host_ptr
<Security_context::set_host_ptr 516
>lex_start
| >LEX::new_top_level_query
| | >LEX::new_query
| | | >alloc_root
| | | <alloc_root 304
| | | >alloc_root
| | | <alloc_root 304
| | | >alloc_root
| | | <alloc_root 304
| | <LEX::new_query 640
| <LEX::new_top_level_query 746
<lex_start 511
>login_connection
| >my_net_set_read_timeout
| | >vio_socket_timeout
| | <vio_socket_timeout 322
| <my_net_set_read_timeout 1046
| >my_net_set_write_timeout
| | >vio_socket_timeout
| | <vio_socket_timeout 322
| <my_net_set_write_timeout 1057
| >Security_context::host
| <Security_context::host 98
| >Security_context::host
| <Security_context::host 98
| >Security_context::set_host_or_ip_ptr
| <Security_context::set_host_or_ip_ptr 189
| >Security_context::set_ip_ptr
| <Security_context::set_ip_ptr 561
| >vio_keepalive
| <vio_keepalive 374
| >my_raw_malloc
| <my_raw_malloc 219
| >mysql_audit_acquire_plugins
| <mysql_audit_acquire_plugins 1121
| >acl_authenticate
| | >Security_context::host_or_ip
| | <Security_context::host_or_ip 148
| | >Security_context::ip
| | <Security_context::ip 123
| | >Security_context::host
| | <Security_context::host 98
| | >do_auth_once
| | | >native_password_authenticate
| | | | >server_mpvio_write_packet
| | | | | >send_server_handshake_packet
| | | | | | >alloc_root
| | | | | | <alloc_root 304
| | | | | | >net_flush
| | | | | | | >net_write_packet
| | | | | | | | >Query_cache::insert
| | | | | | | | <Query_cache::insert 959
| | | | | | | | >vio_write
| | | | | | | | <vio_write 214
| | | | | | | <net_write_packet 648
| | | | | | <net_flush 228
| | | | | <send_server_handshake_packet 625
| | | | <server_mpvio_write_packet 1790
| | | | >server_mpvio_read_packet
| | | | | >vio_read
| | | | | <vio_read 136
| | | | | >vio_read
| | | | | <vio_read 136
| | | | | >alloc_root
| | | | | <alloc_root 304
| | | | | >my_raw_malloc
| | | | | <my_raw_malloc 219
| | | | <server_mpvio_read_packet 1903
| | | <native_password_authenticate 2759
| | <do_auth_once 1971
| | >Security_context::assign_user
| | | >my_raw_malloc
| | | <my_raw_malloc 219
| | <Security_context::assign_user 493
| | >my_free
| | <my_free 292
| | >Security_context::user
| | <Security_context::user 73
| | >shutdown_active_vio
| | <shutdown_active_vio 2550
| | >shutdown_active_vio
| | <shutdown_active_vio 2550
| | >mysql_audit_acquire_plugins
| | <mysql_audit_acquire_plugins 1121
| | >Security_context::assign_proxy_user
| | <Security_context::assign_proxy_user 701
| | >Security_context::skip_grants
| | | >Security_context::set_host_or_ip_ptr
| | | <Security_context::set_host_or_ip_ptr 189
| | | >Security_context::assign_priv_user
| | | <Security_context::assign_priv_user 673
| | | >Security_context::assign_priv_host
| | | <Security_context::assign_priv_host 729
| | <Security_context::skip_grants 79
| | >set_ok_status
| | <set_ok_status 396
| | >Security_context::user
| | <Security_context::user 73
| | >Security_context::host_or_ip
| | <Security_context::host_or_ip 148
| <acl_authenticate 2566
| >mysql_audit_acquire_plugins
| <mysql_audit_acquire_plugins 1121
| >send_statement_status
| | >Protocol_classic::send_ok
| | | >net_send_ok
| | | | >net_flush
| | | | | >net_write_packet
| | | | | | >Query_cache::insert
| | | | | | <Query_cache::insert 959
| | | | | | >vio_write
| | | | | | <vio_write 214
| | | | | <net_write_packet 648
| | | | <net_flush 228
| | | <net_send_ok 374
| | <Protocol_classic::send_ok 644
| <send_statement_status 4725
| >my_net_set_read_timeout
| | >vio_socket_timeout
| | <vio_socket_timeout 322
| <my_net_set_read_timeout 1046
| >my_net_set_write_timeout
| | >vio_socket_timeout
| | <vio_socket_timeout 322
| <my_net_set_write_timeout 1057
<login_connection 749
>Security_context::priv_user
<Security_context::priv_user 236
>Security_context::host_or_ip
<Security_context::host_or_ip 148
>my_raw_malloc
<my_raw_malloc 219
>my_hash_first_from_hash_value
<my_hash_first_from_hash_value 319
>plugin_var_memalloc_session_update
<plugin_var_memalloc_session_update 3385
>my_hash_first_from_hash_value
<my_hash_first_from_hash_value 319
>plugin_var_memalloc_session_update
<plugin_var_memalloc_session_update 3385
>ha_enable_transaction
| >commit_owned_gtids(...)
| <commit_owned_gtids(...) 1600
| >ha_commit_trans
| | >ha_commit_low
| | <ha_commit_low 1939
| | >Transaction_ctx::cleanup
| | | >Rpl_transaction_ctx::cleanup
| | | <Rpl_transaction_ctx::cleanup 40
| | | >Transaction_context_log_event::clear_write_set
| | | <Transaction_context_log_event::clear_write_set 50
| | | >free_root
| | | <free_root 477
| | <Transaction_ctx::cleanup 388
| <ha_commit_trans 1849
| >trans_commit_implicit
| | >ha_commit_low
| | | >Transaction_ctx::cleanup
| | | | >Rpl_transaction_ctx::cleanup
| | | | <Rpl_transaction_ctx::cleanup 40
| | | | >Transaction_context_log_event::clear_write_set
| | | | <Transaction_context_log_event::clear_write_set 50
| | | | >free_root
| | | | <free_root 477
| | | <Transaction_ctx::cleanup 388
| | <ha_commit_low 1939
| | >Rpl_consistency_ctx::notify_after_transaction_commit
| | <Rpl_consistency_ctx::notify_after_transaction_commit 64
| <trans_commit_implicit 332
<ha_enable_transaction 5016
>do_command
| >clear_error
| <clear_error 3371
| >reset_diagnostics_area
| <reset_diagnostics_area 371
| >my_net_set_read_timeout
| | >vio_socket_timeout
| | <vio_socket_timeout 322
| <my_net_set_read_timeout 1046
| >vio_read
| <vio_read 136
| >PROFILING::status_change
| <PROFILING::status_change 364
| >vio_read
| <vio_read 136
| >my_raw_malloc
| <my_raw_malloc 219
| >my_free
| <my_free 292
| >my_net_set_read_timeout
| | >vio_socket_timeout
| | <vio_socket_timeout 322
| <my_net_set_read_timeout 1046
| >dispatch_command
| | >PROFILING::start_new_query
| | <PROFILING::start_new_query 393
| | >Security_context::priv_user
| | <Security_context::priv_user 236
| | >Security_context::host_or_ip
| | <Security_context::host_or_ip 148
| | >mysql_audit_acquire_plugins
| | <mysql_audit_acquire_plugins 1121
| | >alloc_root
| | <alloc_root 304
| | >Security_context::priv_user
| | <Security_context::priv_user 236
| | >Security_context::host_or_ip
| | <Security_context::host_or_ip 148
| | >PROFILING::set_query_source
| | <PROFILING::set_query_source 520
| | >alloc_root
| | <alloc_root 304
| | >mysql_parse
| | | >mysql_reset_thd_for_next_command
| | | | >clear_error
| | | | <clear_error 3371
| | | | >reset_diagnostics_area
| | | | <reset_diagnostics_area 371
| | | | >reset_current_stmt_binlog_format_row
| | | | | >set_current_stmt_binlog_format_row
| | | | | <set_current_stmt_binlog_format_row 3661
| | | | <reset_current_stmt_binlog_format_row 3698
| | | | >THD::set_trans_pos
| | | | <THD::set_trans_pos 2778
| | | <mysql_reset_thd_for_next_command 5360
| | | >lex_start
| | | | >LEX::new_top_level_query
| | | | | >LEX::new_query
| | | | | | >alloc_root
| | | | | | <alloc_root 304
| | | | | | >alloc_root
| | | | | | <alloc_root 304
| | | | | | >alloc_root
| | | | | | <alloc_root 304
| | | | | <LEX::new_query 640
| | | | <LEX::new_top_level_query 746
| | | <lex_start 511
| | | >reset_diagnostics_area
| | | <reset_diagnostics_area 371
| | | >free_root
| | | <free_root 477
| | | >mysql_audit_acquire_plugins
| | | <mysql_audit_acquire_plugins 1121
| | | >Query_cache::send_result_to_client
| | | <Query_cache::send_result_to_client 1941
| | | >parse_sql
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >find_sys_var_ex
| | | | | >my_hash_first_from_hash_value
| | | | | <my_hash_first_from_hash_value 319
| | | | <find_sys_var_ex 2800
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >set_stmt_unsafe
| | | | <set_stmt_unsafe 2147
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >set_stmt_unsafe
| | | | <set_stmt_unsafe 2147
| | | <parse_sql 7229
| | | >reset_diagnostics_area
| | | <reset_diagnostics_area 371
| | | >free_root
| | | <free_root 477
| | | >mysql_audit_acquire_plugins
| | | <mysql_audit_acquire_plugins 1121
| | | >mysql_audit_acquire_plugins
| | | <mysql_audit_acquire_plugins 1121
| | | >Security_context::priv_user
| | | <Security_context::priv_user 236
| | | >Security_context::host_or_ip
| | | <Security_context::host_or_ip 148
| | | >mysql_execute_command
| | | | >reset_diagnostics_area
| | | | <reset_diagnostics_area 371
| | | | >free_root
| | | | <free_root 477
| | | | >deny_updates_if_read_only_option
| | | | | >check_readonly
| | | | | <check_readonly 496
| | | | <deny_updates_if_read_only_option 1031
| | | | >opt_trace_start
| | | | | >Opt_trace_context::start
| | | | | <Opt_trace_context::start 983
| | | | | >opt_trace_disable_if_no_tables_access
| | | | | <opt_trace_disable_if_no_tables_access 441
| | | | <opt_trace_start 223
| | | | >gtid_pre_statement_checks
| | | | | >stmt_causes_implicit_commit
| | | | | <stmt_causes_implicit_commit 246
| | | | <gtid_pre_statement_checks 484
| | | | >stmt_causes_implicit_commit
| | | | <stmt_causes_implicit_commit 246
| | | | >gtid_pre_statement_post_implicit_commit_checks
| | | | | >THD::is_ddl_gtid_compatible
| | | | | <THD::is_ddl_gtid_compatible 10909
| | | | <gtid_pre_statement_post_implicit_commit_checks 597
| | | | >mysql_audit_acquire_plugins
| | | | <mysql_audit_acquire_plugins 1121
| | | | >open_temporary_tables
| | | | <open_temporary_tables 7128
| | | | >check_access
| | | | | >PROFILING::status_change
| | | | | <PROFILING::status_change 364
| | | | <check_access 880
| | | | >open_tables_for_query
| | | | | >open_tables
| | | | | | >PROFILING::status_change
| | | | | | <PROFILING::status_change 364
| | | | | | >my_hash_free
| | | | | | <my_hash_free 185
| | | | | | >my_hash_free
| | | | | | <my_hash_free 185
| | | | | <open_tables 5922
| | | | <open_tables_for_query 6499
| | | | >alloc_root
| | | | <alloc_root 304
| | | | >handle_query
| | | | | >PROFILING::status_change
| | | | | <PROFILING::status_change 364
| | | | | >SELECT_LEX::prepare
| | | | | | >st_select_lex::setup_tables
| | | | | | <st_select_lex::setup_tables 804
| | | | | | >alloc_root
| | | | | | <alloc_root 304
| | | | | | >setup_fields
| | | | | | <setup_fields 8960
| | | | | | >SELECT_LEX::setup_conds
| | | | | | <SELECT_LEX::setup_conds 1228
| | | | | | >flatten_subqueries
| | | | | | <flatten_subqueries 2557
| | | | | | >SELECT_LEX::apply_local_transforms
| | | | | | | >simplify_joins
| | | | | | | <simplify_joins 1627
| | | | | | | >record_join_nest_info
| | | | | | | <record_join_nest_info 1677
| | | | | | | >build_bitmap_for_nested_joins
| | | | | | | <build_bitmap_for_nested_joins 4731
| | | | | | <SELECT_LEX::apply_local_transforms 508
| | | | | <SELECT_LEX::prepare 394
| | | | | >lock_tables
| | | | | | >THD::decide_logging_format
| | | | | | <THD::decide_logging_format 10796
| | | | | <lock_tables 6603
| | | | | >Query_cache::store_query
| | | | | | >THD::is_classic_protocol
| | | | | | <THD::is_classic_protocol 3382
| | | | | | >Query_cache::is_cacheable
| | | | | | <Query_cache::is_cacheable 3867
| | | | | <Query_cache::store_query 1469
| | | | | >SELECT_LEX::optimize
| | | | | | >alloc_root
| | | | | | <alloc_root 304
| | | | | | >JOIN::optimize
| | | | | | | >PROFILING::status_change
| | | | | | | <PROFILING::status_change 364
| | | | | | | >alloc_func_list
| | | | | | | | >alloc_root
| | | | | | | | <alloc_root 304
| | | | | | | <alloc_func_list 3062
| | | | | | | >JOIN::make_tmp_tables_info
| | | | | | | <JOIN::make_tmp_tables_info 3917
| | | | | | <JOIN::optimize 353
| | | | | <SELECT_LEX::optimize 1019
| | | | | >JOIN::exec
| | | | | | >PROFILING::status_change
| | | | | | <PROFILING::status_change 364
| | | | | | >JOIN::prepare_result
| | | | | | <JOIN::prepare_result 912
| | | | | | >send_result_metadata
| | | | | | | >Protocol_classic::start_result_metadata
| | | | | | | | >alloc_root
| | | | | | | | <alloc_root 304
| | | | | | | <Protocol_classic::start_result_metadata 1058
| | | | | | | >Protocol_classic::send_field_metadata
| | | | | | | <Protocol_classic::send_field_metadata 1189
| | | | | | | >Protocol_classic::end_row
| | | | | | | <Protocol_classic::end_row 1198
| | | | | | <send_result_metadata 4660
| | | | | | >Protocol_classic::end_result_metadata
| | | | | | <Protocol_classic::end_result_metadata 1085
| | | | | | >Query_result_send::send_data
| | | | | | | >send_result_set_row
| | | | | | | | >my_raw_malloc
| | | | | | | | <my_raw_malloc 219
| | | | | | | <send_result_set_row 4685
| | | | | | <Query_result_send::send_data 2724
| | | | | | >Protocol_classic::end_row
| | | | | | <Protocol_classic::end_row 1198
| | | | | | >set_eof_status
| | | | | | <set_eof_status 422
| | | | | <JOIN::exec 172
| | | | | >PROFILING::status_change
| | | | | <PROFILING::status_change 364
| | | | | >st_select_lex_unit::cleanup
| | | | | | >st_select_lex::cleanup()
| | | | | | | >JOIN::cleanup
| | | | | | | <JOIN::cleanup 2634
| | | | | | <st_select_lex::cleanup() 1092
| | | | | <st_select_lex_unit::cleanup 944
| | | | <handle_query 204
| | | | >PROFILING::status_change
| | | | <PROFILING::status_change 364
| | | | >mysql_audit_acquire_plugins
| | | | <mysql_audit_acquire_plugins 1121
| | | | >trans_commit_stmt
| | | | | >ha_commit_low
| | | | | <ha_commit_low 1939
| | | | | >Rpl_consistency_ctx::notify_after_transaction_commit
| | | | | <Rpl_consistency_ctx::notify_after_transaction_commit 64
| | | | <trans_commit_stmt 474
| | | | >st_select_lex_unit::cleanup
| | | | | >st_select_lex::cleanup()
| | | | | | >JOIN::destroy
| | | | | | <JOIN::destroy 975
| | | | | <st_select_lex::cleanup() 1092
| | | | <st_select_lex_unit::cleanup 944
| | | | >PROFILING::status_change
| | | | <PROFILING::status_change 364
| | | | >close_thread_tables
| | | | <close_thread_tables 1724
| | | | >stmt_causes_implicit_commit
| | | | <stmt_causes_implicit_commit 246
| | | | >MDL_context::release_transactional_locks
| | | | | >MDL_context::release_locks_stored_before
| | | | | <MDL_context::release_locks_stored_before 4439
| | | | | >MDL_context::release_locks_stored_before
| | | | | <MDL_context::release_locks_stored_before 4439
| | | | <MDL_context::release_transactional_locks 4718
| | | | >binlog_gtid_end_transaction
| | | | | >stmt_causes_implicit_commit
| | | | | <stmt_causes_implicit_commit 246
| | | | <binlog_gtid_end_transaction 2394
| | | <mysql_execute_command 5106
| | | >~opt_trace_start
| | | <~opt_trace_start 232
| | | >PROFILING::status_change
| | | <PROFILING::status_change 364
| | | >lex_end
| | | <lex_end 534
| | | >Query_arena::free_items
| | | | >Item_result_field::cleanup()
| | | | | >Item::cleanup
| | | | | <Item::cleanup 797
| | | | <Item_result_field::cleanup() 10808
| | | | >my_free
| | | | <my_free 292
| | | | >Item::cleanup
| | | | <Item::cleanup 797
| | | | >Item::cleanup
| | | | <Item::cleanup 797
| | | <Query_arena::free_items 3395
| | <mysql_parse 5647
| | >send_statement_status
| | | >Protocol_classic::send_eof
| | | | >net_send_ok
| | | | | >net_flush
| | | | | | >net_write_packet
| | | | | | | >Query_cache::insert
| | | | | | | <Query_cache::insert 959
| | | | | | | >vio_write
| | | | | | | <vio_write 214
| | | | | | <net_write_packet 648
| | | | | <net_flush 228
| | | | <net_send_ok 374
| | | <Protocol_classic::send_eof 672
| | <send_statement_status 4725
| | >Rpl_consistency_ctx::notify_after_response_packet
| | <Rpl_consistency_ctx::notify_after_response_packet 147
| | >Query_cache::end_of_result
| | <Query_cache::end_of_result 1056
| | >mysql_audit_acquire_plugins
| | <mysql_audit_acquire_plugins 1121
| | >mysql_audit_acquire_plugins
| | <mysql_audit_acquire_plugins 1121
| | >mysql_audit_acquire_plugins
| | <mysql_audit_acquire_plugins 1121
| | >log_slow_applicable
| | <log_slow_applicable 1707
| | >PROFILING::status_change
| | <PROFILING::status_change 364
| | >free_root
| | <free_root 477
| | >PROFILING::finish_current_profile
| | <PROFILING::finish_current_profile 450
| <dispatch_command 1928
<do_command 1007
>do_command
| >clear_error
| <clear_error 3371
| >reset_diagnostics_area
| <reset_diagnostics_area 371
| >my_net_set_read_timeout
| | >vio_socket_timeout
| | <vio_socket_timeout 322
| <my_net_set_read_timeout 1046
| >vio_read
| | >vio_io_wait

```