CFLAGS := -I. -DPURPLE_PLUGINS -fpic -g -Wall
CFLAGS += $(shell pkg-config --cflags purple)
LDFLAGS := $(shell pkg-config --libs purple) -fpic
TARGET := libwhatsapp.so
VERSION := $(shell cat whatsappprpl.h | sed -n 's/.*DISPLAY_VERSION.*"\(.*\)"/\1/p')
CFILES   := $(foreach dir,.,$(notdir $(wildcard $(dir)/*.c)))
OBJECTS = $(CFILES:%.c=%.o)

.PHONY: all
all: $(TARGET)

$(TARGET): $(OBJECTS)
	$(CC) -shared $(OBJECTS) $(LDFLAGS) -o $(TARGET)

%.o: %.c
	@echo $(notdir $<)
	$(CC) $(CFLAGS) -c $< -o $@


clean:
	rm -f $(TARGET)
	rm -f $(OBJECTS)

install:
	cp libwhatsapp.so ~/.purple/plugins/

sdist:
	tar -cvjpf whatsapppurple-$(VERSION).tar.bz2 data src Makefile*
