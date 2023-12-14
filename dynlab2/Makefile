CXX = g++
CXXFLAGS = -Wall -g -fPIC
LIBS = -lsqlite3

SRCDIR = .
INCDIR = .
BUILDDIR = build
BINDIR = bin

TARGET = $(BINDIR)/dynlab2
SOURCES = $(wildcard $(SRCDIR)/*.cpp)
OBJECTS = $(patsubst $(SRCDIR)/%.cpp, $(BUILDDIR)/%.o, $(SOURCES))
DEPS = $(OBJECTS:.o=.d)

LIBDIR = lib
LIBNAME = librenovation.so
DYNAMICLIB = $(LIBDIR)/$(LIBNAME)

.PHONY: all clean

all: $(TARGET)

$(TARGET): $(DYNAMICLIB) $(OBJECTS)
	@mkdir -p $(BINDIR)
	$(CXX) $(CXXFLAGS) $(OBJECTS) -o $@ $(LIBS) -L$(LIBDIR) -Wl,-rpath=$(LIBDIR) -lrenovation

$(BUILDDIR)/%.o: $(SRCDIR)/%.cpp
	@mkdir -p $(BUILDDIR)
	$(CXX) $(CXXFLAGS) -I$(INCDIR) -MMD -MP -c $< -o $@

$(DYNAMICLIB): $(BUILDDIR)/Renovation.o
	@mkdir -p $(LIBDIR)
	$(CXX) -shared $(CXXFLAGS) -o $@ $^

clean:
	rm -rf $(BUILDDIR) $(BINDIR) $(LIBDIR)

-include $(DEPS)