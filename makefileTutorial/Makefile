.DEFAULT_GOAL := all

TARGET    := my_app
BUILD_DIR := build
SRC_DIR   := src
INC_DIR   := include

SRC_FILES := $(wildcard $(SRC_DIR)/*.c)
OBJ_FILES := $(patsubst $(SRC_DIR)/%.c, $(BUILD_DIR)/%.o, $(SRC_FILES))
DEPS      := $(OBJ_FILES:.o=.d)


CC = gcc
CPPFLAGS := -I$(INC_DIR)
CFLAGS   := -std=c11 -Wall -Wextra -Wpedantic
LDFLAGS  :=
LDLIBS   := -lm

BUILD ?= release
ifeq ($(BUILD), debug)
	CFLAGS += -O0 -g3
else ifeq ($(BUILD), release)
	CFLAGS += -O2
else
	$(error invalid BUILD='$(BUILD)')
endif

CPPFLAGS += -MMD -MP

.PHONY: all clean rebuild

all: $(BUILD_DIR)/$(TARGET)

$(BUILD_DIR)/$(TARGET): $(OBJ_FILES) | $(BUILD_DIR)
	$(CC) $(LDFLAGS) -o $@ $^ $(LDLIBS)
#	gcc -o build/my_app build/main.o build/myMath.o -lm

$(BUILD_DIR)/%.o: $(SRC_DIR)/%.c | $(BUILD_DIR)
	$(CC) $(CPPFLAGS) $(CFLAGS) -c $< -o $@
#	gcc -Iinclude -MMP -MP -std=c11 -Wall -Wextra -Wpedantic -c main.c -o build/main.o
#	gcc -Iinclude -MMP -MP -std=c11 -Wall -Wextra -Wpedantic -c myMath.c -o build/myMath.o
$(BUILD_DIR):
	mkdir -p $@
#	mkdir -p build
-include $(DEPS)

clean:
	rm -rf $(BUILD_DIR)

rebuild: clean all


