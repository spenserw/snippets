MKDIR_P = mkdir -p

DEPS = $(wildcard include/*)
SRC = $(filter %.cpp,$(wildcard src/*))

OBJDIR=src/obj
_OBJS = $(notdir $(subst .cpp,.o,$(SRC))) # sources => objects
OBJS=$(patsubst %,$(OBJDIR)/%,$(_OBJS)) # prepend `OBJDIR` to objects


CC = g++
CFLAGS := -std=c++17 -Wall -Iinclude/ -Ithirdparty/
LFLAGS = -Llib/

BIN_NAME = APP_NAME_HERE

all: directories $(BIN_NAME)

$(OBJDIR)/%.o: src/%.cpp $(DEPS)
	$(CC) -c -o $@ $< $(CFLAGS)

.PHONY: directories
directories: $(OBJDIR)

$(OBJDIR):
	${MKDIR_P} $(OBJDIR)

$(BIN_NAME): $(OBJS)
	$(CC) -o $(BIN_NAME) $(OBJS) $(CFLAGS) $(LFLAGS)

.PHONY: debug
debug : CFLAGS += -ggdb
debug : $(OBJS) 
	$(CC) -o $(BIN_NAME) $(OBJS) $(CFLAGS) $(LFLAGS)

.PHONY: clean
clean:
	rm -f $(OBJDIR)/*.o
