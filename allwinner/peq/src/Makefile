target			= libpeq.so

INCLUDES        += -I. -I./include -I./crypto
LIBS            += -lpthread -ldl -lcrypto

SRCS = eq.c eq_mid.c cJSON.c

install:
	-@mkdir -p $(CONFIG_PREFIX)/usr/lib
	-@mkdir -p $(CONFIG_PREFIX)/usr/include
	@cp ./eq.h $(CONFIG_PREFIX)/usr/include
	@cp ./eq_mid.h $(CONFIG_PREFIX)/usr/include
	@cp ./cJSON.h $(CONFIG_PREFIX)/usr/include

#libpeq.so
$(target): $(SRCS)
	$(CC) -fPIC -shared $(INCLUDES) $(LDFLAGS) $^ -o $@ $(LIBS)
	@cp $@ $(CONFIG_PREFIX)/usr/lib

####################################################################
all: install $(target)
clean:
	rm -rf $(target)
