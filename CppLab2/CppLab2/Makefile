CXX = g++
CXXFLAGS = -Wall -g -fPIC
LIBS = -lsqlite3

SRCDIR = .
INCDIR = .
BUILDDIR = build
BINDIR = bin

TARGET = $(BINDIR)/my_program
SOURCES = $(wildcard $(SRCDIR)/*.cpp)
OBJECTS = $(patsubst $(SRCDIR)/%.cpp, $(BUILDDIR)/%.o, $(SOURCES))
DEPS = $(OBJECTS:.o=.d)

LIBDIR = lib
LIBNAME = libemployee.so
DYNAMICLIB = $(LIBDIR)/$(LIBNAME)

.PHONY: all clean

all: $(TARGET)

$(TARGET): $(DYNAMICLIB) $(OBJECTS)
	@mkdir -p $(BINDIR)
	$(CXX) $(CXXFLAGS) $(OBJECTS) -o $@ $(LIBS) -L$(LIBDIR) -Wl,-rpath=$(LIBDIR) -lemployee

$(BUILDDIR)/%.o: $(SRCDIR)/%.cpp
	@mkdir -p $(BUILDDIR)
	$(CXX) $(CXXFLAGS) -I$(INCDIR) -MMD -MP -c $< -o $@

$(DYNAMICLIB): $(BUILDDIR)/Employee.o
	@mkdir -p $(LIBDIR)
	$(CXX) -shared $(CXXFLAGS) -o $@ $^

clean:
	rm -rf $(BUILDDIR) $(BINDIR) $(LIBDIR)

-include $(DEPS)