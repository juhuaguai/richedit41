
# NT build environment
# Allow for customization through a decoration file
!IFDEF NTMAKEENV
!include $(NTMAKEENV)\makefile.def
!ENDIF

!IF EXIST("makefile.cfg")
!INCLUDE "makefile.cfg"
!ENDIF

# The following builds are supported

!IF "$(BUILD)" == "" 
BUILD=w32_x86_dbg
!MESSAGE No Build specified. Defaulting to w32_x86_dbg
!ENDIF

!IF "$(ODIR)" == ""
ODIR = .\
!MESSAGE No output directory specified.  Defaulting to current directory
!ENDIF

TOMINC=tom41
DLLBASENAME=msftedit
DEFFILENAME=msftedit

!IF "$(BUILD)" == "w32_x86_dbg"

DEFFILENAME=msfteditd
INCLUDE = $(INCLUDE) 
CFLAGS = -DDEBUG -Od -DNOACCESSIBILITY -DNODELAYLOAD
CFLAGS = $(CFLAGS) -DWIN32 -D_WINDOWS -D_X86_ -DWINNT
CFLAGS = $(CFLAGS) -Gz -Gm -Zi
LFLAGS = $(LFLAGS) ..\lib\x86\usp10.lib
LFLAGS = $(LFLAGS) kernel32.lib
LFLAGS = $(LFLAGS) advapi32.lib
LFLAGS = $(LFLAGS) gdi32.lib
LFLAGS = $(LFLAGS) user32.lib
LFLAGS = /entry:DllMain@12 /debug /base:0x48000000 $(LFLAGS)
CPP = cl $(CFLAGS)
CL = cl $(CFLAGS)
RCFLAGS=  $(USERRCFLAGS) -dINCLUDETLB -dDEBUG
LINKER = link
CHKSTK = ..\lib\x86\chkstk.obj
FTOL = ..\lib\x86\ftol2.obj
MEMMOVE = ..\lib\x86\memmove.obj
MEMSET = ..\lib\x86\memset.obj
MEMCMP = ..\lib\x86\memcmp.obj
MEMCPY = ..\lib\x86\memcpy.obj
STRLEN = ..\lib\x86\strlen.obj

!ELSEIF "$(BUILD)" == "w32_x86_shp"

INCLUDE = $(INCLUDE)
CFLAGS = -O1 $(USERDEFS)
CFLAGS = $(CFLAGS) -DWIN32 -D_WINDOWS -D_X86_ -DWINNT
CFLAGS = $(CFLAGS) -GFz
LFLAGS = 
LFLAGS = $(LFLAGS) ..\lib\x86\usp10.lib -delayload:usp10.dll -delay:unload
LFLAGS = $(LFLAGS) kernel32.lib
LFLAGS = $(LFLAGS) advapi32.lib
LFLAGS = $(LFLAGS) gdi32.lib
LFLAGS = $(LFLAGS) user32.lib
LFLAGS = /opt:ref /incremental:no /entry:DllMain@12 /base:0x48000000 $(LFLAGS)
CPP = cl $(CFLAGS)
CL = cl $(CFLAGS)
LINKER = link
RCFLAGS=  $(USERRCFLAGS) -dINCLUDETLB
CHKSTK = ..\lib\x86\chkstk.obj
FTOL = ..\lib\x86\ftol2.obj
MEMMOVE = ..\lib\x86\memmove.obj
MEMSET = ..\lib\x86\memset.obj
MEMCMP = ..\lib\x86\memcmp.obj
MEMCPY = ..\lib\x86\memcpy.obj
STRLEN = ..\lib\x86\strlen.obj

!ELSEIF "$(BUILD)" == "w64_IA64_dbg"

!MESSAGE Building 64 bit version in debug flavor

CFLAGS = -DDEBUG -Od -DNOACCESSIBILITY
CFLAGS = $(CFLAGS) -DWIN64 -D_WINDOWS -D_IA64_ -DWINNT 
CFLAGS = $(CFLAGS) -Gz -Gm -Zi
LFLAGS =
LFLAGS = $(LFLAGS) ..\win64lib\msls31.lib delayload.lib -delayload:msls31.dll
LFLAGS = $(LFLAGS) ..\win64lib\usp10.lib -delayload:usp10.dll -delay:unload
LFLAGS = $(LFLAGS) kernel32.lib
LFLAGS = $(LFLAGS) advapi32.lib
LFLAGS = $(LFLAGS) gdi32.lib
LFLAGS = $(LFLAGS) user32.lib
LFLAGS = $(LFLAGS) libcmt.lib
LFLAGS = /entry:_DllMainCRTStartup -machine:ia64 $(LFLAGS)
LFLAGS = $(LFLAGS) /DEBUG
CPP = cl $(CFLAGS)
CL = cl $(CFLAGS)
RCFLAGS=  $(USERRCFLAGS) -dINCLUDETLB -dDEBUG -d_WIN64
LINKER = link

!ELSEIF "$(BUILD)" == "wce_cepc_dbg"

TOMINC=tomce
DLLBASENAME=ebriched
PATH = \msdev\wce\bin;$(PATH)
PATH = \Program^ Files\DevStudio\wce\bin;$(PATH)
INCLUDE = ..\wceinc
CFLAGS = -DDEBUG -Od -Z7
CFLAGS = $(CFLAGS) -DWIN32 -D_WINDOWS -DUNDER_CE -DEBOOK_CE
CFLAGS = $(CFLAGS) -D_X86_ -Dx86
CPP = cl386 $(CFLAGS)
CL = cl386 $(CFLAGS)
LIB = ..\wcelib\x86
LINKER = link
LFLAGS = $(LFLAGS) msls31.lib coredll.lib corelibc.lib oleaut32.lib
LFLAGS = -nodefaultlib -subsystem:windowsce,2.12 -entry:_DllMainCRTStartup /debug:full /debugtype:cv -machine:x86 -ignore:4078 $(LFLAGS)

!ELSEIF "$(BUILD)" == "wce_cepc_shp"

TOMINC=tomce
DLLBASENAME=ebriched
PATH = \msdev\wce\bin;$(PATH)
PATH = \Program^ Files\DevStudio\wce\bin;$(PATH)
INCLUDE = ..\wceinc
CFLAGS = -O1 $(USERDEFS)
CFLAGS = $(CFLAGS) -DWIN32 -D_WINDOWS -DUNDER_CE -DEBOOK_CE
CFLAGS = $(CFLAGS) -D_X86_ -Dx86
CFLAGS = $(CFLAGS) -GFz

CPP = cl386 $(CFLAGS)
CL = cl386 $(CFLAGS)
LINKER = link
LIB = ..\wcelib\x86
LFLAGS = $(LFLAGS) msls31.lib coredll.lib corelibc.lib oleaut32.lib
LFLAGS = -opt:ref -nodefaultlib -subsystem:windowsce,2.12 -entry:_DllMainCRTStartup -machine:x86 -ignore:4078 $(LFLAGS)

!ELSE

!ERROR $(BUILD) Unknown Build.  Need to learn this one.

!ENDIF 

INCLUDE = .;..\inc41;..\lsinc;..\$(TOMINC);$(INCLUDE)
CFLAGS = $(USERCFLAGS) $(CFLAGS) -DUNICODE -nologo
CFLAGS = $(CFLAGS) -Zl -W4 -Ob1 -FR -GX-
CFLAGS = $(CFLAGS) -YX_common.h

LFLAGS = $(USERLFLAGS) $(LFLAGS) /nologo
LFLAGS = /implib:msftedit.lib /def:$(DEFFILENAME).def /ignore:4078 /map /NODEFAULTLIB:uuid.lib $(LFLAGS)
LFLAGS = /dll /out:$(ODIR)\$(DLLBASENAME).dll $(LFLAGS)

.c{$(ODIR)}.obj:
	cl $(CFLAGS) /c -Fo$@ $<

.cpp{$(ODIR)}.obj:
	cl $(CFLAGS) /c -Fo$@ $<

all: _version.h all1

all1: $(ODIR)\w32sys.obj \
	$(ODIR)\utilmem.obj \
	$(ODIR)\dxfrobj.obj \
	$(ODIR)\tomsel.obj \
	$(ODIR)\dispml.obj \
	$(ODIR)\doc.obj \
    $(ODIR)\rtflex.obj \
	$(ODIR)\render.obj \
	$(ODIR)\dispprt.obj \
	$(ODIR)\measure.obj \
	$(ODIR)\util.obj \
    $(ODIR)\host.obj \
	$(ODIR)\select.obj \
	$(ODIR)\callmgr.obj \
	$(ODIR)\dfreeze.obj \
    $(ODIR)\rtext.obj \
	$(ODIR)\rtfwrit.obj \
	$(ODIR)\propchg.obj \
	$(ODIR)\m_undo.obj \
	$(ODIR)\rtfwrit2.obj \
    $(ODIR)\clasifyc.obj \
	$(ODIR)\cmsgflt.obj \
	$(ODIR)\ime.obj \
	$(ODIR)\magellan.obj \
	$(ODIR)\layout.obj \
	$(ODIR)\text.obj \
	$(ODIR)\runptr.obj \
    $(ODIR)\disp.obj \
	$(ODIR)\format.obj \
	$(ODIR)\antievt.obj \
	$(ODIR)\reinit.obj \
    $(ODIR)\objmgr.obj \
	$(ODIR)\ldte.obj \
	$(ODIR)\rtfread2.obj \
    $(ODIR)\dragdrp.obj \
	$(ODIR)\urlsup.obj \
	$(ODIR)\CFPF.obj \
	$(ODIR)\uuid.obj \
    $(ODIR)\frunptr.obj \
	$(ODIR)\edit.obj \
	$(ODIR)\line.obj \
	$(ODIR)\TOMFMT.obj \
    $(ODIR)\dispsl.obj \
	$(ODIR)\coleobj.obj \
	$(ODIR)\object.obj \
	$(ODIR)\osdc.obj \
	$(ODIR)\tomrange.obj \
    $(ODIR)\notmgr.obj \
	$(ODIR)\font.obj \
	$(ODIR)\HASH.obj \
	$(ODIR)\hyph.obj \
	$(ODIR)\rtfread.obj \
    $(ODIR)\lbhost.obj \
    $(ODIR)\cbhost.obj \
    $(ODIR)\devdsc.obj \
    $(ODIR)\debug.obj \
	$(ODIR)\range.obj \
	$(ODIR)\array.obj \
	$(ODIR)\TOMDOC.obj \
	$(ODIR)\textserv.obj \
	$(ODIR)\kern.obj \
	$(ODIR)\ols.obj \
	$(ODIR)\olsole.obj \
	$(ODIR)\uspi.obj \
	$(ODIR)\txtbrk.obj \
	$(ODIR)\iaccess.obj \
	$(ODIR)\cuim.obj \
	$(ODIR)\textnot.obj \
	$(CHKSTK) \
	$(FTOL) \
	$(MEMMOVE) \
	$(MEMSET) \
	$(MEMCMP) \
	$(MEMCPY) \
	$(STRLEN)
	
	rc $(RCFLAGS) msftedit.rc
	$(LINKER) $(LFLAGS) $** msftedit.res
	bscmake /omsftedit.bsc /nologo *.sbr

_version.h: msftedit.rc
	perl version.pl <msftedit.rc >_version.h

clean:
	-del msftedit.dll
	-del *.lib
	-del *.obj
	-del *.sbr
	-del *.pch
	-del *.pdb
	-del *.idb
	-del *.ilk
antievt.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _m_undo.h _callmgr.h textserv.h _edit.h textsrv2.h _ldte.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h  \
	_antievt.h _frunptr.h _text.h _runptr.h _format.h _range.h _rtext.h  \
	_uspi.h usp10.h _select.h

array.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _invar.h

callmgr.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h  \
	_select.h _range.h _text.h _runptr.h _rtext.h _frunptr.h _format.h  \
	_uspi.h usp10.h _disp.h _devdsc.h _line.h _drwinfo.h _dxfrobj.h

cfpf.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _rtfconv.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h  \
	_callmgr.h _dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h  \
	HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h \
	_range.h _text.h _runptr.h _rtext.h _frunptr.h _format.h _uspi.h  \
	usp10.h tokens.h _font.h _kern.h

clasifyc.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _clasfyc.h

cmsgflt.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _MSREMSG.H msctf.h textstor.h ctfutb.h msctfp.h textserv.h  \
	_cmsgflt.h _ime.h _cuim.h _notmgr.h

coleobj.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h  \
	_select.h _range.h _text.h _runptr.h _rtext.h _frunptr.h _format.h  \
	_uspi.h usp10.h _disp.h _devdsc.h _line.h _drwinfo.h _dispprt.h  \
	_dispml.h _layout.h _antievt.h _dxfrobj.h

debug.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h

devdsc.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _devdsc.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h  \
	_callmgr.h _dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h  \
	HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h \
	_font.h _kern.h

dfreeze.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _disp.h _devdsc.h _line.h _runptr.h _doc.h _edit.h  \
	textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h _dragdrp.h _osdc.h \
	_notmgr.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h  \
	_magelln.h _MSREMSG.H _textnot.h _drwinfo.h _dfreeze.h

disp.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _disp.h _devdsc.h _line.h _runptr.h _doc.h _edit.h  \
	textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h _dragdrp.h _osdc.h \
	_notmgr.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h  \
	_magelln.h _MSREMSG.H _textnot.h _drwinfo.h _select.h _range.h  \
	_text.h _rtext.h _frunptr.h _format.h _uspi.h usp10.h _font.h _kern.h \
	_measure.h _ols.h _dfreeze.h _invar.h

dispml.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _dispml.h _disp.h _devdsc.h _line.h _runptr.h _doc.h _edit.h \
	textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h _dragdrp.h _osdc.h \
	_notmgr.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h  \
	_magelln.h _MSREMSG.H _textnot.h _drwinfo.h _layout.h _format.h  \
	_font.h _kern.h _measure.h _rtext.h _text.h _frunptr.h _ols.h usp10.h \
	_render.h _select.h _range.h _uspi.h _dfreeze.h _invar.h

dispprt.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _dispprt.h _dispml.h _disp.h _devdsc.h _line.h _runptr.h  \
	_doc.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _objmgr.h _coleobj.h HWXInk.h msctf.h  \
	textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h _drwinfo.h  \
	_layout.h _format.h _font.h _kern.h _measure.h _rtext.h _text.h  \
	_frunptr.h _ols.h usp10.h _render.h _select.h _range.h _uspi.h

dispsl.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _dispsl.h _disp.h _devdsc.h _line.h _runptr.h _doc.h _edit.h \
	textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h _dragdrp.h _osdc.h \
	_notmgr.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h  \
	_magelln.h _MSREMSG.H _textnot.h _drwinfo.h _measure.h _rtext.h  \
	_text.h _frunptr.h _format.h _ols.h usp10.h _select.h _range.h  \
	_uspi.h _render.h _font.h _kern.h _dfreeze.h

doc.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _doc.h _format.h textserv.h _invar.h

dragdrp.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h _disp.h  \
	_devdsc.h _line.h _runptr.h _drwinfo.h _select.h _range.h _text.h  \
	_rtext.h _frunptr.h _format.h _uspi.h usp10.h _font.h _kern.h  \
	_measure.h _ols.h

dxfrobj.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h  \
	_dxfrobj.h _range.h _text.h _runptr.h _rtext.h _frunptr.h _format.h  \
	_uspi.h usp10.h hash.h tokens.h

edit.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h  \
	_dispprt.h _dispml.h _disp.h _devdsc.h _line.h _runptr.h _drwinfo.h  \
	_layout.h _format.h _dispsl.h _select.h _range.h _text.h _rtext.h  \
	_frunptr.h _uspi.h usp10.h _font.h _kern.h _measure.h _ols.h  \
	_render.h _antievt.h _hyph.h _urlsup.h _dfreeze.h _txtbrk.h  \
	_clasfyc.h

font.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _font.h _kern.h _rtfconv.h _edit.h textserv.h textsrv2.h  \
	_ldte.h _m_undo.h _callmgr.h _dragdrp.h _osdc.h _notmgr.h _doc.h  \
	_objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h  \
	_MSREMSG.H _textnot.h _range.h _text.h _runptr.h _rtext.h _frunptr.h  \
	_format.h _uspi.h usp10.h tokens.h

format.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _format.h textserv.h

frunptr.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h  \
	_frunptr.h _text.h _runptr.h _format.h _rtext.h _font.h _kern.h  \
	_invar.h

hash.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h hash.h tokens.h

host.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _host.h textserv.h textsrv2.h dynarray.h _notmgr.h _format.h \
	_edit.h _ldte.h _m_undo.h _callmgr.h _dragdrp.h _osdc.h _doc.h  \
	_objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h  \
	_MSREMSG.H _textnot.h

ime.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h msctf.h textstor.h ctfutb.h textserv.h _cmsgflt.h _MSREMSG.H \
	_ime.h

ldte.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _range.h _text.h _runptr.h _doc.h textserv.h _m_undo.h  \
	_callmgr.h _rtext.h _edit.h textsrv2.h _ldte.h _dragdrp.h _osdc.h  \
	_notmgr.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h  \
	_magelln.h _MSREMSG.H _textnot.h _frunptr.h _format.h _uspi.h usp10.h \
	_antievt.h _disp.h _devdsc.h _line.h _drwinfo.h _select.h _dxfrobj.h  \
	_rtfwrit.h _rtfconv.h tokens.h _rtfread.h _rtflog.h _urlsup.h  \
	_dfreeze.h

layout.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _dispml.h _disp.h _devdsc.h _line.h _runptr.h _doc.h _edit.h \
	textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h _dragdrp.h _osdc.h \
	_notmgr.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h  \
	_magelln.h _MSREMSG.H _textnot.h _drwinfo.h _layout.h _format.h  \
	_select.h _range.h _text.h _rtext.h _frunptr.h _uspi.h usp10.h  \
	_measure.h _ols.h _render.h

line.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _line.h _runptr.h _doc.h _measure.h _rtext.h _edit.h  \
	textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h _dragdrp.h _osdc.h \
	_notmgr.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h  \
	_magelln.h _MSREMSG.H _textnot.h _text.h _frunptr.h _format.h _disp.h \
	_devdsc.h _drwinfo.h _ols.h usp10.h _render.h _dispml.h _layout.h

m_undo.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _m_undo.h _callmgr.h textserv.h _edit.h textsrv2.h _ldte.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h _disp.h  \
	_devdsc.h _line.h _runptr.h _drwinfo.h _urlsup.h _dfreeze.h _range.h  \
	_text.h _rtext.h _frunptr.h _format.h _uspi.h usp10.h _antievt.h

magellan.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h _disp.h  \
	_devdsc.h _line.h _runptr.h _drwinfo.h

measure.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _measure.h _rtext.h _edit.h textserv.h textsrv2.h _ldte.h  \
	_m_undo.h _callmgr.h _dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h  \
	_coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H \
	_textnot.h _text.h _runptr.h _frunptr.h _format.h _line.h _disp.h  \
	_devdsc.h _drwinfo.h _ols.h usp10.h _font.h _kern.h _layout.h _uspi.h

notmgr.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _notmgr.h

object.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h _rtext.h \
	_text.h _runptr.h _frunptr.h _format.h _select.h _range.h _uspi.h  \
	usp10.h _disp.h _devdsc.h _line.h _drwinfo.h

objmgr.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h  \
	_notmgr.h _m_undo.h _callmgr.h textserv.h _edit.h textsrv2.h _ldte.h  \
	_dragdrp.h _osdc.h _doc.h _magelln.h _MSREMSG.H _textnot.h _disp.h  \
	_devdsc.h _line.h _runptr.h _drwinfo.h _select.h _range.h _text.h  \
	_rtext.h _frunptr.h _format.h _uspi.h usp10.h

osdc.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _osdc.h

propchg.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h  \
	_dispprt.h _dispml.h _disp.h _devdsc.h _line.h _runptr.h _drwinfo.h  \
	_layout.h _format.h _dispsl.h _select.h _range.h _text.h _rtext.h  \
	_frunptr.h _uspi.h usp10.h _font.h _kern.h _measure.h _ols.h  \
	_render.h _urlsup.h _dfreeze.h

range.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _range.h _text.h _runptr.h _doc.h textserv.h _m_undo.h  \
	_callmgr.h _rtext.h _edit.h textsrv2.h _ldte.h _dragdrp.h _osdc.h  \
	_notmgr.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h  \
	_magelln.h _MSREMSG.H _textnot.h _frunptr.h _format.h _uspi.h usp10.h \
	_antievt.h _disp.h _devdsc.h _line.h _drwinfo.h _rtfconv.h tokens.h  \
	_txtbrk.h _font.h _kern.h _ols.h _invar.h

reinit.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _font.h _kern.h _format.h textserv.h _disp.h _devdsc.h  \
	_line.h _runptr.h _doc.h _edit.h textsrv2.h _ldte.h _m_undo.h  \
	_callmgr.h _dragdrp.h _osdc.h _notmgr.h _objmgr.h _coleobj.h HWXInk.h \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h  \
	_drwinfo.h _clasfyc.h _rtfconv.h _range.h _text.h _rtext.h _frunptr.h \
	_uspi.h usp10.h tokens.h _ols.h _host.h dynarray.h _version.h

render.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _render.h _measure.h _rtext.h _edit.h textserv.h textsrv2.h  \
	_ldte.h _m_undo.h _callmgr.h _dragdrp.h _osdc.h _notmgr.h _doc.h  \
	_objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h  \
	_MSREMSG.H _textnot.h _text.h _runptr.h _frunptr.h _format.h _line.h  \
	_disp.h _devdsc.h _drwinfo.h _ols.h usp10.h _font.h _kern.h _select.h \
	_range.h _uspi.h _layout.h

rtext.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h  \
	_frunptr.h _text.h _runptr.h _format.h _rtext.h _disp.h _devdsc.h  \
	_line.h _drwinfo.h _select.h _range.h _uspi.h usp10.h _antievt.h  \
	_txtbrk.h _invar.h

rtflex.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _rtfread.h _rtfconv.h _edit.h textserv.h textsrv2.h _ldte.h  \
	_m_undo.h _callmgr.h _dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h  \
	_coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H \
	_textnot.h _range.h _text.h _runptr.h _rtext.h _frunptr.h _format.h  \
	_uspi.h usp10.h tokens.h _rtflog.h hash.h tokens.cpp

rtflog.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _rtflog.h tokens.h

rtfread.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _rtfread.h _rtfconv.h _edit.h textserv.h textsrv2.h _ldte.h  \
	_m_undo.h _callmgr.h _dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h  \
	_coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H \
	_textnot.h _range.h _text.h _runptr.h _rtext.h _frunptr.h _format.h  \
	_uspi.h usp10.h tokens.h _rtflog.h _font.h _kern.h _disp.h _devdsc.h  \
	_line.h _drwinfo.h rtflog.cpp

rtfread2.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _rtfread.h _rtfconv.h _edit.h textserv.h textsrv2.h _ldte.h  \
	_m_undo.h _callmgr.h _dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h  \
	_coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H \
	_textnot.h _range.h _text.h _runptr.h _rtext.h _frunptr.h _format.h  \
	_uspi.h usp10.h tokens.h _rtflog.h _disp.h _devdsc.h _line.h  \
	_drwinfo.h _dxfrobj.h

rtfwrit.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _rtfwrit.h _rtfconv.h _edit.h textserv.h textsrv2.h _ldte.h  \
	_m_undo.h _callmgr.h _dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h  \
	_coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H \
	_textnot.h _range.h _text.h _runptr.h _rtext.h _frunptr.h _format.h  \
	_uspi.h usp10.h tokens.h _font.h _kern.h _dispml.h _disp.h _devdsc.h  \
	_line.h _drwinfo.h _layout.h _version.h

rtfwrit2.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _rtfwrit.h _rtfconv.h _edit.h textserv.h textsrv2.h _ldte.h  \
	_m_undo.h _callmgr.h _dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h  \
	_coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H \
	_textnot.h _range.h _text.h _runptr.h _rtext.h _frunptr.h _format.h  \
	_uspi.h usp10.h tokens.h

runptr.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _runptr.h _doc.h _text.h textserv.h _m_undo.h _callmgr.h  \
	_invar.h

select.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _select.h _range.h _text.h _runptr.h _doc.h textserv.h  \
	_m_undo.h _callmgr.h _rtext.h _edit.h textsrv2.h _ldte.h _dragdrp.h  \
	_osdc.h _notmgr.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h  \
	ctfutb.h _magelln.h _MSREMSG.H _textnot.h _frunptr.h _format.h  \
	_uspi.h usp10.h _disp.h _devdsc.h _line.h _drwinfo.h _measure.h  \
	_ols.h _font.h _kern.h _rtfconv.h tokens.h _antievt.h _invar.h

text.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _text.h _runptr.h _doc.h textserv.h _m_undo.h _callmgr.h  \
	_edit.h textsrv2.h _ldte.h _dragdrp.h _osdc.h _notmgr.h _objmgr.h  \
	_coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H \
	_textnot.h _antievt.h _frunptr.h _format.h _clasfyc.h _txtbrk.h  \
	_invar.h

textserv.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h  \
	_dispprt.h _dispml.h _disp.h _devdsc.h _line.h _runptr.h _drwinfo.h  \
	_layout.h _format.h _dispsl.h _select.h _range.h _text.h _rtext.h  \
	_frunptr.h _uspi.h usp10.h _font.h _kern.h _measure.h _ols.h  \
	_render.h _antievt.h _urlsup.h _dfreeze.h _clasfyc.h _tomfmt.h  \
	_dxfrobj.h

tokens.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h tokens.h

tomdoc.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _range.h _text.h _runptr.h _doc.h textserv.h _m_undo.h  \
	_callmgr.h _rtext.h _edit.h textsrv2.h _ldte.h _dragdrp.h _osdc.h  \
	_notmgr.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h  \
	_magelln.h _MSREMSG.H _textnot.h _frunptr.h _format.h _uspi.h usp10.h \
	_disp.h _devdsc.h _line.h _drwinfo.h _rtfconv.h tokens.h _select.h  \
	_font.h _kern.h _tomfmt.h

tomfmt.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _tomfmt.h _range.h _text.h _runptr.h _doc.h textserv.h  \
	_m_undo.h _callmgr.h _rtext.h _edit.h textsrv2.h _ldte.h _dragdrp.h  \
	_osdc.h _notmgr.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h  \
	ctfutb.h _magelln.h _MSREMSG.H _textnot.h _frunptr.h _format.h  \
	_uspi.h usp10.h _font.h _kern.h

tomrange.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _select.h _range.h _text.h _runptr.h _doc.h textserv.h  \
	_m_undo.h _callmgr.h _rtext.h _edit.h textsrv2.h _ldte.h _dragdrp.h  \
	_osdc.h _notmgr.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h  \
	ctfutb.h _magelln.h _MSREMSG.H _textnot.h _frunptr.h _format.h  \
	_uspi.h usp10.h _line.h _tomfmt.h _disp.h _devdsc.h _drwinfo.h  \
	_measure.h _ols.h _invar.h

tomsel.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _select.h _range.h _text.h _runptr.h _doc.h textserv.h  \
	_m_undo.h _callmgr.h _rtext.h _edit.h textsrv2.h _ldte.h _dragdrp.h  \
	_osdc.h _notmgr.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h  \
	ctfutb.h _magelln.h _MSREMSG.H _textnot.h _frunptr.h _format.h  \
	_uspi.h usp10.h _disp.h _devdsc.h _line.h _drwinfo.h _invar.h

urlsup.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h  \
	_urlsup.h _dfreeze.h _range.h _text.h _runptr.h _rtext.h _frunptr.h  \
	_format.h _uspi.h usp10.h _select.h _clasfyc.h

util.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _rtfconv.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h  \
	_callmgr.h _dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h  \
	HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h \
	_range.h _text.h _runptr.h _rtext.h _frunptr.h _format.h _uspi.h  \
	usp10.h tokens.h

uuid.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h

ols.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h _font.h  \
	_kern.h _render.h _measure.h _rtext.h _text.h _runptr.h _frunptr.h  \
	_format.h _line.h _disp.h _devdsc.h _drwinfo.h _ols.h usp10.h  \
	_tomfmt.h _range.h _uspi.h _clasfyc.h _txtbrk.h _hyph.h

lbhost.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _host.h textserv.h textsrv2.h dynarray.h _notmgr.h _format.h \
	_edit.h _ldte.h _m_undo.h _callmgr.h _dragdrp.h _osdc.h _doc.h  \
	_objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h  \
	_MSREMSG.H _textnot.h _cbhost.h

cbhost.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _host.h textserv.h textsrv2.h dynarray.h _notmgr.h _format.h \
	_edit.h _ldte.h _m_undo.h _callmgr.h _dragdrp.h _osdc.h _doc.h  \
	_objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h  \
	_MSREMSG.H _textnot.h _cbhost.h

uspi.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _font.h _kern.h _edit.h textserv.h textsrv2.h _ldte.h  \
	_m_undo.h _callmgr.h _dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h  \
	_coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H \
	_textnot.h _frunptr.h _text.h _runptr.h _format.h _select.h _range.h  \
	_rtext.h _uspi.h usp10.h _measure.h _line.h _disp.h _devdsc.h  \
	_drwinfo.h _ols.h

txtbrk.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h  \
	_frunptr.h _text.h _runptr.h _format.h _range.h _rtext.h _uspi.h  \
	usp10.h _txtbrk.h

iaccess.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _host.h textserv.h textsrv2.h dynarray.h _notmgr.h _cbhost.h

w32sys.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _host.h textserv.h textsrv2.h dynarray.h _notmgr.h _font.h  \
	_kern.h _edit.h _ldte.h _m_undo.h _callmgr.h _dragdrp.h _osdc.h  \
	_doc.h _objmgr.h _coleobj.h HWXInk.h msctf.h textstor.h ctfutb.h  \
	_magelln.h _MSREMSG.H _textnot.h w32win32.cpp aimm.h aimmex.h  \
	aimm_i.c _uspi.h usp10.h w32wince.cpp

w32win32.obj : \
	aimm.h aimmex.h msctf.h textstor.h ctfutb.h aimm_i.c _font.h _kern.h  \
	_array.h _uspi.h _ls.h usp10.h

utilmem.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h

cuim.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _MSREMSG.H msctf.h textstor.h ctfutb.h ctffunc.h msctf_g.c  \
	cicclsid.c msctf_i.c textstor_i.c ctffunc_i.c msctfp.h msctfp_g.c  \
	textserv.h _cmsgflt.h _ime.h _cuim.h _notmgr.h dcattrs.h

textnot.obj : \
	_common.h _debug.h resource.h _util.h _cfpf.h _ls.h _w32sys.h  \
	_array.h _edit.h textserv.h textsrv2.h _ldte.h _m_undo.h _callmgr.h  \
	_dragdrp.h _osdc.h _notmgr.h _doc.h _objmgr.h _coleobj.h HWXInk.h  \
	msctf.h textstor.h ctfutb.h _magelln.h _MSREMSG.H _textnot.h

