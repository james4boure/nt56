SRC_NAME=lzma-4.65

# 检查 HOST_NCPU 是否定义，如果没有定义，默认为 1
ifndef HOST_NCPU
  HOST_NCPU=1
endif

all:
	@if [ ! -d "$(SRC_NAME)/CPP/7zip/Compress/LZMA_Alone" ]; then \
		echo "Source directory $(SRC_NAME)/CPP/7zip/Compress/LZMA_Alone not found!"; \
		exit 1; \
	fi
	make -j$(HOST_NCPU) -C $(SRC_NAME)/CPP/7zip/Compress/LZMA_Alone -f makefile.gcc || { echo "Build failed"; exit 1; }
	cp $(SRC_NAME)/CPP/7zip/Compress/LZMA_Alone/lzma ./lzma

clean:
	make -C $(SRC_NAME)/CPP/7zip/Compress/LZMA_Alone -f makefile.gcc clean
	rm -f lzma
