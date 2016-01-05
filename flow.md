1.build lj_vm.S from vm_<arch>.dasc
2.hotloop or hotcall to dec hotcount, if count < 0 then call lj_trace_hot to entry tracing mode
3.record bytecode to ssa ir(lj_record_ins in lj_record.c)

