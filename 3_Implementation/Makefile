PROJ_FOL = Stepin-PhoneBook_system
PROJ_NAME = PhoneBook_system
TEST_PROJ_NAME = test_$(PROJ_NAME)

BUILD_DIR = Build

SRC = src/phonebook1.c

TEST_SRC = test/test_phonebook1.c\
unity/unity.c

TEST_OUTPUT = $(BUILD)/test_$(PROJ_NAME).out

INC = -I inc -I unity

#To check if the OS is Windows or Linux and set the executable file extension and delete command accordingly
ifdef OS
   RM = del /q
   FixPath = $(subst /,\,$1)
   EXEC = exe
else
   ifeq ($(shell uname), Linux)
      RM = rm -rf
      FixPath = $1
	  EXEC = out
   endif
endif

# Makefile will not run target command if the name with file already exists. To override, use .PHONY
.PHONY : all test coverage run clean doc
# -lm is for definitaion of pow in math.h

all:$(BUILD_DIR)
	gcc main1.c $(SRC) $(INC) -o $(call FixPath,$(BUILD_DIR)/$(PROJ_NAME).$(EXEC)) -lm 

run: all
	$(call FixPath,$(BUILD_DIR)/$(PROJ_NAME).$(EXEC))

test: $(SRC) $(TEST_SRC)
	gcc $^ $(INC) -o $(call FixPath,$(BUILD_DIR)/$(TEST_PROJ_NAME).$(EXEC)) -lm
	$(call FixPath,$(BUILD_DIR)/$(TEST_PROJ_NAME).$(EXEC))

# coverage:${PROJECT_NAME}
# 	gcc main1.c -fprofile-arcs -ftest-coverage $(SRC) $(INC) -o $(call FixPath,$(BUILD_DIR)/$(TEST_PROJ_NAME).$(EXEC)) -lm
# 	$(call FixPath,$(BUILD_DIR)/$(TEST_PROJ_NAME).$(EXEC))
# 	gcov -a main1.c

coverageCheck:$(BUILD)
	gcc -fprofile-arcs -ftest-coverage -fPIC -O0 $(SRC) $(TEST_SRC) $(INC) -o $(BUILD_DIR)$(TEST_OUTPUT)
	./$(BUILD_DIR)/$(TEST_OUTPUT)

# coverage:
# 	cp test/test_phonebook1.c .
# 	gcc -fprofile-arcs -ftest-coverage $(INC) unity/unity.c test_contacts1.c $(SRC) -o $(call FixPath, $(TEST_PROJ_NAME).$(EXEC))
# 	$(call FixPath, ./$(TEST_PROJ_NAME).$(EXEC))
# 	gcov -a $(COV_SRC)
# 	$(RM) *.$(EXEC)
# 	$(RM) *.gcda
# 	$(RM) *.gcno
# 	$(RM) *.c.gcov
# 	$(RM) *.DAT
# 	$(RM) test_phonebook1.c

doc:
	make -C doc
$(BUILD_DIR):
	mkdir $(BUILD_DIR)

clean:
	$(RM) $(call FixPath,$(BUILD_DIR)/*)
	make clean -C doc
	rmdir $(BUILD_DIR) doc/html
