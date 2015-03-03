CC := clpru
AR := arpru
 
#OBJECTS = $(patsubst %.c,%.o,$(wildcard drivers/*.c))
OBJECTS = \
	drivers/cpsw.o	   drivers/elm.o      drivers/hs_mmcsd.o  drivers/phy.o      drivers/uart_irda_cir.o \
	drivers/dcan.o	   drivers/gpio_v2.o  drivers/mailbox.o   drivers/raster.o   drivers/watchdog.o \
	drivers/dmtimer.o  drivers/gpmc.o     drivers/mcspi.o	  drivers/rtc.o \
	drivers/ecap.o	   drivers/hsi2c.o    drivers/mdio.o	  drivers/tsc_adc.o
SOURCES = $(patsubst %o,%c,$(OBJECTS)) include/*.h include/hw/*.h
 
SRCTAR = pru_am335x_starterware.tgz
 
TARGETDIR = build/pru
TARGET = $(TARGETDIR)/libstarterware.a
INCLUDEDIR = -Iinclude -Iinclude/hw -I/usr/share/ti/cgt-pru/include
 
CFLAGS := -O3 $(INCLUDEDIR)
 
$(TARGET): $(OBJECTS)
	mkdir -p $(TARGETDIR)
	rm -f $@
	$(AR) a $@ $(OBJECTS)
 
%.o: %.c
	$(CC) -c --output_file=$@ $< $(CFLAGS)
 
install: $(TARGET)
	sudo install -m 755 -d /usr/share/pru_am335x_starterware/lib
	sudo install -m 644 -t /usr/share/pru_am335x_starterware/lib $(TARGET)
	sudo install -m 755 -d /usr/share/pru_am335x_starterware/include
	sudo install -m 644 -t /usr/share/pru_am335x_starterware/include include/*.h
	sudo install -m 755 -d /usr/share/pru_am335x_starterware/include/hw
	sudo install -m 644 -t /usr/share/pru_am335x_starterware/include/hw include/hw/*.h
 
$(SRCTAR) package:
	tar czf $(SRCTAR) $(SOURCES) Makefile --transform "s#^#pru_am335x_starterware/#"
 
.PHONY: clean
 
clean:
	rm -f $(OBJECTS) $(TARGET) $(SRCTAR)
