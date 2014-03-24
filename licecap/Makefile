OBJDIR    =   obj
C_FILES = WDL/WDL/giflib/dgif_lib.c \
	WDL/WDL/giflib/egif_lib.c \
	WDL/WDL/giflib/gif_hash.c \
	WDL/WDL/giflib/gifalloc.c \
	WDL/WDL/zlib/adler32.c \
	WDL/WDL/zlib/compress.c \
	WDL/WDL/zlib/crc32.c \
	WDL/WDL/zlib/deflate.c \
	WDL/WDL/zlib/infback.c \
	WDL/WDL/zlib/inffast.c \
	WDL/WDL/zlib/inflate.c \
	WDL/WDL/zlib/inftrees.c \
	WDL/WDL/zlib/trees.c \
	WDL/WDL/zlib/uncompr.c \
	WDL/WDL/zlib/zutil.c \
	WDL/WDL/win32_utf8.c

CPP_FILES = WDL/WDL/lice/lice_gif.cpp \
	WDL/WDL/lice/lice.cpp \
	WDL/WDL/lice/lice_arc.cpp \
	WDL/WDL/lice/lice_gif_write.cpp \
	WDL/WDL/lice/lice_lcf.cpp \
	WDL/WDL/lice/lice_line.cpp \
	WDL/WDL/lice/lice_palette.cpp \
	WDL/WDL/lice/lice_text.cpp \
	WDL/WDL/filebrowse.cpp \
	WDL/WDL/wingui/wndsize.cpp \
	licecap_ui.cpp

RCR   = rc.exe /dCURLDEBUG=0
RESFLAGS = /i../include

ifdef SYSTEMROOT
	RM = del /Q
	CC = cl
	LIBS = user32.lib shell32.lib gdi32.lib advapi32.lib winmm.lib comdlg32.lib
	OBJSUF = .obj
	LINK_FLAGS = /Fe$(OBJDIR)/licecap
	CFLAGS = /Fo$@
else
	RM = rm -f
	CC = g++
	CFLAGS = -o $@
	OBJSUF = .o
	LINK_FLAGS = -o $(OBJDIR)/licecap
endif

OBJ_FILES := $(addprefix $(OBJDIR)/,$(CPP_FILES:.cpp=$(OBJSUF))) $(addprefix $(OBJDIR)/,$(C_FILES:.c=$(OBJSUF)))

all: $(OBJDIR) licecap.exe

$(OBJDIR):
	mkdir -p $(addprefix obj/,$(dir $(CPP_FILES) $(C_FILES)))

licecap.exe: $(OBJ_FILES) $(OBJDIR)/licecap.res
	$(CC) $(LINK_FLAGS) $^ $(LIBS)

$(OBJDIR)/%$(OBJSUF): %.cpp
	$(CC) -c $(CFLAGS) $(CPPFLAGS) $<

$(OBJDIR)/%$(OBJSUF): %.c
	$(CC) -c $(CFLAGS) $(CPPFLAGS) $<

$(OBJDIR)/licecap.res : licecap.rc icon1.ico
	$(RCR) $(RESFLAGS) /Fo"$@" licecap.rc

clean:
	rm -rf $(OBJDIR)/

test:
	@echo $(addprefix obj/, $(subst /,_,$(CPP_FILES:.cpp=.obj)))
