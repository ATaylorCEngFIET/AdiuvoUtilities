#make sure you export the name of the top module using command export TOP=

CORE_DIR = ../rtl
CORETB_DIR = .
MODELSIMINI = C:/modelsim_dlx64_2020.4/modelsim.ini
RTL_SOURCES := $(wildcard $(CORE_DIR)/*.vhd)
TB_SOURCES := $(wildcard $(CORETB_DIR)/*.vhd)

print-%  : 
	@echo $* = $($*)

%.vhdl: %.vhd
	vcom -modelsimini $(MODELSIMINI) -2008 +cover=bcesft -work work $<

libs: 
	vlib work
	vmap work work

compile_tb:$(TB_SOURCES)
	vcom -modelsimini $(MODELSIMINI) -2008 +cover=bcesft -work work $^

compile_rtl:$(RTL_SOURCES)
	vcom -modelsimini $(MODELSIMINI) -2008 +cover=bcesft -work work $^  

run_sim: $(TB_SOURCES) $(RTL_SOURCES)
	vsim -coverage -l $(TOP).log -t ps $(TOP) -do "run -all"
	#quit
	coverage report -details -output $(TOP).txt -assert -directive -cvg -codeAll
	exit

run_sim_debug: $(TB_SOURCES) $(RTL_SOURCES)
	vsim -coverage -l $(TOP).log -t ps $(TOP)

bps:
	BluePearlCLI $(RTL_SOURCES) -output Results -tcl analysis.tcl

clean:
	\rm  -rf work/*
#(C:/GIT/realtra_fpga/CLK_RST_CNTRL/rtl)(/)(([a-z0-9_-]*)*)