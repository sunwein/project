CC = gcc
CPP = g++
AR = ar

CFLAGS= -Wall -O2 -std=c++11  #-g             #编译选项
CFLAGS +=-I./include                #编译选项
LDFLAGS = -lmemcached               #链接选项
ARFLAGS = -rc                       #归档选项

LIBPATH =$(PROJECT_HOME)/lib/
APPPATH =$(PROJECT_HOME)/app/

SLIB = $(LIBPATH)libredis.a
DLIB = $(LIBPATH)libfun.so
EXEC = $(APPPATH)client.exe

SPATH =./
SRCS := $(wildcard *.cpp)
# $(SPATH)client.cpp
#	   $(SPATH)fun2.c  \
#	   $(SPATH)fun3.c  
#SRCS +=$(SPATH)test.c

OBJS := $(patsubst %cpp,%o,$(SRCS))

%.o:%.cpp  
	$(CPP) $(CFLAGS) -c $<

EXEC:$(OBJS)                         #生成可执行程序，依赖于OBJS
	$(CPP) $(CFLAGS) $(OBJS) -o  $(EXEC) $(LDFLAGS)
	@echo "Create Application ($(EXEC)) successful..."

SLIB:$(OBJS)                         #生成静态链接库，依赖于OBJS
	$(AR) $(ARFLAGS) $(SLIB) $(OBJS)
	@echo "Create staticlib ($(SLIB)) successful..."

DLIB:$(OBJS)                         #生成动态链接库，依赖于OBJS
	$(CC) -fpic -shared -o $(DLIB) $(OBJS)
	@echo "Create sharelib ($(DLIB)) successful..."

clean:                               #清除相关文件
	rm -rf $(OBJS) $(SLIB) $(EXEC) $(DLIB)

#只需修改 SRCS  SLIB  EXEC  DLIB  SPATH
#生成应用程序命令:make
#生成静态链接库命令：make SLIB
#生成动态链接库命令：make DLIB
#在makefile所在的目录新建app,lib,include,src四个目录
#分别用于存放应用程序，链接库，头文件，源文件
