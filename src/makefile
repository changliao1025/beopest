####################  System  ####################
VPATH=../src
#  Fortran compiler
FC=gfortran -c -O3 -DUNIX -DFLUSHFILE
#  C compiler
CC=cc  -c -O3 -DUNIX
#  Linker
LD=gfortran -O3
#  Archive
AR=ar -rcs
LDFLAGS=
#  Compile With MPI
FM=mpif90 -c -O3 -DUNIX -DFLUSHFILE -DBEOMPI
LM=mpif90 -O3
LMFLAGS=
#  Compile Without MPI
#FM=gfortran -c -O3 -DUNIX -DFLUSHFILE
#LM=gfortran -O3
####################  Definitions  ####################
PEST=pest ppest supcalc
SENS=sensan senschek
UTL1=eigproc inschek jacwrit jco2jco jcotrans jcochek par2par paramfix parrep pestchek jcosub pestgen picalc ppause pslave pstop pstopst punpause svdaprep tempchek wtfactor ppd2asc ppd2par
UTL2=parcalc obscalc
UTL3=dercomb1 genlin jco2mat jcoaddz jcocomb jcoorder jcopcat jrow2mat jrow2vec obsrep paramerr pclc2mat pcov2mat pest2vec pestlin prederr prederr1 prederr2 pwtadj1 regerr resproc reswrit scalepar vec2pest veclog prederr3 pwtadj2 jcodiff regpred addreg1 randpar mulpartab comfilnme paramid postjactest genlinpred subreg1 phistats lhs2pest pest2lhs parreduce assesspar
UTL4=cov2cor covcond mat2srf matadd matcolex matdiag matdiff matinvp matjoinc matjoind matjoinr matorder matprod matquad matrow matsmul matspec matsvd matsym mattrans matxtxi matxtxix mat2jco
UTL5=cmaes_p sceua_p jactest rdmulres obs2obs
#UTL6=supobspar supobsprep supobspar1
EXE=$(PEST) $(UTL1) $(UTL2) $(UTL3) $(UTL4) $(UTL5) $(UTL6) $(SENS)

#  Commonly use functions
COMMON=space.o pgetcl.o nblnk.o openun.o orthog.o linpos.o lapack1.o writsig.o common.o pestwait.o msleep.o matman.o random.o randgen.o slinpos.o
#  Pest functions shared by all versions of pest
SHARED=pestsub1.o writall.o writint.o pardef.o drealrd.o optwt.o cgsolve.o compress.o readpest.o lsqr.o pestdata.o modrun.o pestsub2.o common_mod.o ms_stubs.o common.a

all:$(EXE)

clean:
	rm -f *.a *.o *.mod

clean_all:
	rm -f *.a *.o *.mod *.exe $(EXE)

clean_exe:
	rm -f *.exe $(EXE)

install:$(EXE)
	cp -a $(EXE) ../bin
#cp -a $(EXE) $(OSHOME)/bin

####################  Dependencies  ####################
.SUFFIXES: .o .c .f .F .F90
.F90.o:
	$(FC) $<
.F.o:
	$(FC) $<
.f.o:
	$(FC) $<
.c.o:
	$(CC) $<

####################  Linker Commands  ####################
#  Archive of commonly used functions
common.a: $(COMMON)
	$(AR) $@ $^
#  Sequential PEST
pest:       pest.o dercalc.o runpest.o $(SHARED)
	$(LD) -o $@ $^ $(LDFLAGS)
#  Parallel PEST
ppest:      pest_par.o dercalc_par.o runpest_par.o beopest.o beorun.o ip.o parpest.o numdays.o $(SHARED)
	$(LM) -o $@ $^ $(LMFLAGS)
#  SupCalc
supcalc:    supcalc.o  readpest.o compress.o certfile.o pestdata.o common.a;$(LD) -o $@ $^ $(LDFLAGS)
#  Sensitivity
sensan:     sensan.o sensub.o      common.a;$(LD) -o $@ $^ $(LDFLAGS)
senschek:   senschek.o scheksub.o  common.a;$(LD) -o $@ $^ $(LDFLAGS)
#  Utility 1
pslave:     pslave.o sstop.o       common.a;$(LD) -o $@ $^ $(LDFLAGS)
pestchek:   pestchek.o cheksub.o   common.a;$(LD) -o $@ $^ $(LDFLAGS)
eigproc:    eigproc.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
inschek:    inschek.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
jacwrit:    jacwrit.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
jco2jco:    jco2jco.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
jcotrans:   jcotrans.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
par2par:    par2par.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
paramfix:   paramfix.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
parrep:     parrep.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
pestgen:    pestgen.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
picalc:     picalc.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
ppause:     ppause.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
pstop:      pstop.o                common.a;$(LD) -o $@ $^ $(LDFLAGS)
pstopst:    pstopst.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
punpause:   punpause.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
svdaprep:   svdaprep.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
tempchek:   tempchek.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
wtfactor:   wtfactor.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
ppd2asc:    ppd2asc.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
ppd2par:    ppd2par.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
#  Utility 2
parcalc:    parcalc.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
obscalc:    obscalc.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
#  Utility 3
dercomb1:   dercomb1.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
genlin:     genlin.o                common.a;$(LD) -o $@ $^ $(LDFLAGS)
jco2mat:    jco2mat.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
jcoaddz:    jcoaddz.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
jcoorder:   jcoorder.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
jcopcat:    jcopcat.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
jrow2mat:   jrow2mat.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
jrow2vec:   jrow2vec.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
obsrep:     obsrep.o                common.a;$(LD) -o $@ $^ $(LDFLAGS)
paramerr:   paramerr.o  certfile.o  common.a;$(LD) -o $@ $^ $(LDFLAGS)
pclc2mat:   pclc2mat.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
pcov2mat:   pcov2mat.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
pest2vec:   pest2vec.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
pestlin:    pestlin.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
prederr:    prederr.o   certfile.o  common.a;$(LD) -o $@ $^ $(LDFLAGS)
prederr1:   prederr1.o  certfile.o  common.a;$(LD) -o $@ $^ $(LDFLAGS)
prederr2:   prederr2.o  certfile.o  common.a;$(LD) -o $@ $^ $(LDFLAGS)
pwtadj1:    pwtadj1.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
regerr:     regerr.o    certfile.o  common.a;$(LD) -o $@ $^ $(LDFLAGS)
resproc:    resproc.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
reswrit:    reswrit.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
scalepar:   scalepar.o  certfile.o  common.a;$(LD) -o $@ $^ $(LDFLAGS)
vec2pest:   vec2pest.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
veclog:     veclog.o                common.a;$(LD) -o $@ $^ $(LDFLAGS)
prederr3:   prederr3.o  certfile.o  common.a;$(LD) -o $@ $^ $(LDFLAGS)
pwtadj2:    pwtadj2.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
jcodiff:    jcodiff.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
jcochek:    jcochek.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
jcocomb:    jcocomb.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
jcosub:     jcosub.o                common.a;$(LD) -o $@ $^ $(LDFLAGS)
regpred:    regpred.o   certfile.o  common.a;$(LD) -o $@ $^ $(LDFLAGS)
addreg1:    addreg1.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
randpar:    randpar.o   certfile.o  common.a;$(LD) -o $@ $^ $(LDFLAGS)
mulpartab:  mulpartab.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
comfilnme:  comfilnme.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
paramid:    paramid.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
postjactest:postjactest.o           common.a;$(LD) -o $@ $^ $(LDFLAGS)
genlinpred: genlinpred.o certfile.o common.a;$(LD) -o $@ $^ $(LDFLAGS)
subreg1:    subreg1.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
phistats:   phistats.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
lhs2pest:   lhs2pest.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
pest2lhs:   pest2lhs.o   certfile.o common.a;$(LD) -o $@ $^ $(LDFLAGS)
parreduce:  parreduce.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
assesspar:  assesspar.o  certfile.o common.a;$(LD) -o $@ $^ $(LDFLAGS)

#  Utility 4
cov2cor:    cov2cor.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
covcond:    covcond.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
mat2srf:    mat2srf.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
matadd:     matadd.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
matcolex:   matcolex.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
matdiag:    matdiag.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
matdiff:    matdiff.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
matinvp:    matinvp.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
matjoinc:   matjoinc.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
matjoind:   matjoind.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
matjoinr:   matjoinr.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
matorder:   matorder.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
matprod:    matprod.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
matquad:    matquad.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
matrow:     matrow.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
matsmul:    matsmul.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
matspec:    matspec.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
matsvd:     matsvd.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
matsym:     matsym.o               common.a;$(LD) -o $@ $^ $(LDFLAGS)
mattrans:   mattrans.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
matxtxi:    matxtxi.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
matxtxix:   matxtxix.o             common.a;$(LD) -o $@ $^ $(LDFLAGS)
mat2jco:    mat2jco.o              common.a;$(LD) -o $@ $^ $(LDFLAGS)
#  Utility 5
cmaes_p:    cmaes_p.o cmaes.o readpest.o common.o pestsub1.o writint.o mio.o compress.o prm.o pestdata.o certread.o slapack.o ms_stubs.o common.a;$(LD) -o $@ $^ $(LDFLAGS)
sceua_p:    sceua_p.o sceua.o readpest.o common.o pestsub1.o writint.o mio.o compress.o prm.o pestdata.o                                 common.a;$(LD) -o $@ $^ $(LDFLAGS)
jactest:    jactest.o         readpest.o common.o pestsub1.o writint.o mio.o compress.o prm.o pestdata.o                                 common.a;$(LD) -o $@ $^ $(LDFLAGS)
rdmulres:   rdmulres.o                            pestsub1.o writint.o mio.o                                                             common.a;$(LD) -o $@ $^ $(LDFLAGS)
obs2obs:    obs2obs.o eqn.o                                  writint.o mio.o                                                             common.a;$(LD) -o $@ $^ $(LDFLAGS)
#  Utility 6 (array_btree chokes gfortran)
#supobsprep: supobsprep.o array_btree.o common.a;$(LD) -o $@ $^ $(LDFLAGS)
#  Auto-generated dependencies

beopest.mod beopriv.mod beorun_data.mod: beopest.o
cmaes_module.mod: cmaes.o
common_mod.mod: common_mod.o
equation.mod: eqn.o
model_input_output_interface.mod: mio.o
svd_parm_data.mod: pardef.o
pestdata.mod: pestdata.o
parallel_run_manager.mod: prm.o
message_utility.mod pdf.mod: random.o
sceua_module.mod: sceua.o
addreg1.o: addreg1.F version.inc
assesspar.o: assesspar.F version.inc
beopest.o: beopest.F beopest.inc pestdata.mod svd_parm_data.mod version.inc;$(FM) $<
beorun.o: beorun.F beopest.mod beopriv.mod beorun_data.mod common_mod.mod pestdata.mod;$(FC) -DPARALLEL -DBEO -o $@ $<
certfile.o: certfile.F
certread.o: certread.F
cgsolve.o: cgsolve.F
cheksub.o: cheksub.F
cmaes.o: cmaes.F90
cmaes_p.o: cmaes_p.F cmaes_module.mod model_input_output_interface.mod parallel_run_manager.mod pestdata.mod version.inc
comfilnme.o: comfilnme.F version.inc
common.o: common.F
common_mod.o: common_mod.F
compress.o: compress.F pestdata.mod
cov2cor.o: cov2cor.F matman.f version.inc
covcond.o: covcond.F matman.f version.inc
dercalc.o: dercalc.F beopest.mod common_mod.mod pestdata.mod
dercalc_par.o: dercalc.F beopest.mod common_mod.mod pestdata.mod;$(FC) -DPARALLEL -DBEO -o $@ $<
dercomb1.o: dercomb1.F version.inc
drealrd.o: drealrd.F
eigproc.o: eigproc.F version.inc
eqn.o: eqn.F90
genlin.o: genlin.F version.inc
genlinpred.o: genlinpred.F version.inc
inschek.o: inschek.F version.inc
ip.o: ip.c
jactest.o: jactest.F model_input_output_interface.mod parallel_run_manager.mod pestdata.mod version.inc
jacwrit.o: jacwrit.F version.inc
jco2jco.o: jco2jco.F version.inc
jco2mat.o: jco2mat.F version.inc
jcoaddz.o: jcoaddz.F version.inc
jcochek.o: jcochek.F version.inc
jcocomb.o: jcocomb.F version.inc
jcodiff.o: jcodiff.F version.inc
jcoorder.o: jcoorder.F version.inc
jcopcat.o: jcopcat.F version.inc
jcosub.o: jcosub.F version.inc
jcotrans.o: jcotrans.F version.inc
jrow2mat.o: jrow2mat.F version.inc
jrow2vec.o: jrow2vec.F version.inc
lapack1.o: lapack1.F
lhs2pest.o: lhs2pest.F version.inc
linpos.o: linpos.F
lsqr.o: lsqr.F pestdata.mod svd_parm_data.mod
mat2jco.o: mat2jco.F matman.f version.inc
mat2srf.o: mat2srf.F version.inc
matadd.o: matadd.F matman.f version.inc
matcolex.o: matcolex.F matman.f version.inc
matdiag.o: matdiag.F matman.f version.inc
matdiff.o: matdiff.F matman.f version.inc
matinvp.o: matinvp.F matman.f version.inc
matjoinc.o: matjoinc.F matman.f version.inc
matjoind.o: matjoind.F matman.f version.inc
matjoinr.o: matjoinr.F matman.f version.inc
matman.o: matman.f
matorder.o: matorder.F matman.f version.inc
matprod.o: matprod.F matman.f version.inc
matquad.o: matquad.F matman.f version.inc
matrow.o: matrow.F matman.f version.inc
matsmul.o: matsmul.F matman.f version.inc
matspec.o: matspec.F matman.f version.inc
matsvd.o: matsvd.F matman.f version.inc
matsym.o: matsym.F matman.f version.inc
mattrans.o: mattrans.F matman.f version.inc
matxtxi.o: matxtxi.F matman.f version.inc
matxtxix.o: matxtxix.F matman.f version.inc
mio.o: mio.F90
modrun.o: modrun.F beopest.mod common_mod.mod pestdata.mod
ms_stubs.o: ms_stubs.F
msleep.o: msleep.c
mulpartab.o: mulpartab.F version.inc
nblnk.o: nblnk.F
numdays.o: numdays.F
obs2obs.o: obs2obs.F equation.mod model_input_output_interface.mod version.inc
obscalc.o: obscalc.F90 inter.inc modio.inc utility.inc version.inc
obsrep.o: obsrep.F version.inc
openun.o: openun.F
optwt.o: optwt.F common_mod.mod pestdata.mod
orthog.o: orthog.F
par2par.o: par2par.F version.inc
paramerr.o: paramerr.F version.inc
paramfix.o: paramfix.F version.inc
paramid.o: paramid.F version.inc
parcalc.o: parcalc.F90 inter.inc modio.inc utility.inc version.inc
pardef.o: pardef.F common_mod.mod pestdata.mod
parpest.o: parpest.F beopest.mod beopriv.mod common_mod.mod pestdata.mod;$(FC) -DPARALLEL -DBEO -o $@ $<
parreduce.o: parreduce.F version.inc
parrep.o: parrep.F version.inc
pclc2mat.o: pclc2mat.F matman.f version.inc
pcov2mat.o: pcov2mat.F version.inc
pest.o: pest.F beopest.mod beorun_data.mod pestdata.mod svd_parm_data.mod version.inc
pest2lhs.o: pest2lhs.F version.inc
pest2vec.o: pest2vec.F version.inc
pest_par.o: pest.F beopest.mod beorun_data.mod pestdata.mod svd_parm_data.mod version.inc;$(FC) -DPARALLEL -DBEO -o $@ $<
pestchek.o: pestchek.F version.inc
pestdata.o: pestdata.F
pestgen.o: pestgen.F version.inc
pestlin.o: pestlin.F version.inc
pestsub1.o: pestsub1.F
pestsub2.o: pestsub2.F common_mod.mod errmsg.inc pestdata.mod
pestwait.o: pestwait.F
pgetcl.o: pgetcl.F
phistats.o: phistats.F version.inc
picalc.o: picalc.F version.inc
postjactest.o: postjactest.F version.inc
ppause.o: ppause.F
ppd2asc.o: ppd2asc.F version.inc
ppd2par.o: ppd2par.F version.inc
prederr.o: prederr.F version.inc
prederr1.o: prederr1.F matman.f version.inc
prederr2.o: prederr2.F matman.f version.inc
prederr3.o: prederr3.F version.inc
prm.o: prm.F90 model_input_output_interface.mod
pslave.o: pslave.F version.inc
pstop.o: pstop.F
pstopst.o: pstopst.F
punpause.o: punpause.F
pwtadj1.o: pwtadj1.F version.inc
pwtadj2.o: pwtadj2.F version.inc
randgen.o: randgen.F
random.o: random.F90
randpar.o: randpar.F message_utility.mod pdf.mod version.inc
rdmulres.o: rdmulres.F model_input_output_interface.mod version.inc
readpest.o: readpest.F beopest.mod pestdata.mod
regerr.o: regerr.F version.inc
regpred.o: regpred.F version.inc
resproc.o: resproc.F version.inc
reswrit.o: reswrit.F version.inc
runpest.o: runpest.F beopest.mod common_mod.mod pestdata.mod svd_parm_data.mod
runpest_par.o: runpest.F beopest.mod common_mod.mod pestdata.mod svd_parm_data.mod;$(FC) -DPARALLEL -DBEO -o $@ $<
scalepar.o: scalepar.F version.inc
sceua.o: sceua.F
sceua_p.o: sceua_p.F model_input_output_interface.mod parallel_run_manager.mod pestdata.mod sceua_module.mod version.inc
scheksub.o: scheksub.F
sensan.o: sensan.F version.inc
senschek.o: senschek.F version.inc
sensub.o: sensub.F
slapack.o: slapack.F
slinpos.o: slinpos.F
space.o: space.F
sstop.o: sstop.F
subreg1.o: subreg1.F version.inc
supcalc.o: supcalc.F pestdata.mod version.inc
svdaprep.o: svdaprep.F version.inc
tempchek.o: tempchek.F version.inc
vec2pest.o: vec2pest.F matman.f version.inc
veclog.o: veclog.F matman.f version.inc
writall.o: writall.F common_mod.mod pestdata.mod
writint.o: writint.F
writsig.o: writsig.F
wtfactor.o: wtfactor.F version.inc
