BOOST=../_3rd/boost_1_48_0
BOOST_LIB_PATH=$(BOOST)/stage/lib
BOOST_LIBS=$(BOOST_LIB_PATH)/libboost_program_options.a $(BOOST_LIB_PATH)/libboost_iostreams.a
UNIVERSAL_FLAGS=-force_cpusubtype_ALL -mmacosx-version-min=13.0 -arch x86_64
SDK_ROOT=`xcrun --show-sdk-path`
FRAMEWORK_PATH=$(SDK_ROOT)/System/Library/Frameworks
JAVA_DIR=`/usr/libexec/java_home`
CFLAGS=-Iinclude -I.. -I../syringe/include -I../xpwn/includes -I../xpwn/dll -F$(FRAMEWORK_PATH) -I$(JAVA_DIR)/include -I$(JAVA_DIR)/include/darwin -I/usr/local/opt/openssl/include -I/usr/local/Cellar/libusb/1.0.26/include -DMUX_BUILD=1 $(UNIVERSAL_FLAGS) -fvisibility=hidden 
TOOL=fuzzy_patcher
DYLIB=jsyringeapi.jnilib
LIBS=bz2 system curl z crypto objc
LIB_FILES=../syringe/syringe/libsyringe.a ../fuzzy_patcher/fuzzy_patcher.a ../xpwn/dmglib.a ../mux_redux/mux_redux.jnilib /usr/local/Cellar/libusb/1.0.26/lib/libusb-1.0.dylib
# builtin libusb not universal 
LINK_FLAGS=-framework IOKit -framework CoreFoundation -lstdc++ -L$(SDK_ROOT)/usr/lib -L/usr/local/lib/ -L. $(LD_FLAGS) -L/usr/local/opt/openssl/lib -L/usr/local/Cellar/libusb/1.0.26/lib
SOURCES=jsyringeapi.c jsyringeapi2.c jsyringeapi3.c

$(DYLIB): $(SOURCES)
	gcc -dynamiclib -o $(DYLIB) $(CFLAGS) $(LINK_FLAGS) $(SOURCES) $(LIB_FILES) $(patsubst %,-l%,$(LIBS)) $(BOOST_LIBS) -lusb-1.0
	#gcc -c $(CFLAGS) $(SOURCES)
	#libtool -dynamic -o $(DYLIB) -Wl,-mmin=1 $(LINK_FLAGS) $(patsubst %.c,%.o, $(SOURCES)) $(LIB_FILES) $(patsubst %,-l%,$(LIBS)) $(BOOST_LIBS)

otherDylib:
	cp ../mux_redux/mux_redux.jnilib .

all: $(DYLIB) otherDylib

clean:
	rm *.o *.jnilib
