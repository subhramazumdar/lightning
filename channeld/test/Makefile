# Note that these actually #include everything they need, except ccan/ and bitcoin/.
# That allows for unit testing of statics, and special effects.
CHANNELD_TEST_SRC := $(wildcard channeld/test/run-*.c)
CHANNELD_TEST_OBJS := $(CHANNELD_TEST_SRC:.c=.o)
CHANNELD_TEST_PROGRAMS := $(CHANNELD_TEST_OBJS:.o=)

ALL_TEST_PROGRAMS += $(CHANNELD_TEST_PROGRAMS)
ALL_OBJS += $(CHANNELD_TEST_OBJS)

CHANNELD_TEST_COMMON_OBJS :=			\
	common/amount.o				\
	common/daemon_conn.o			\
	common/htlc_state.o			\
	common/htlc_trim.o			\
	common/htlc_tx.o			\
	common/initial_commit_tx.o		\
	common/key_derive.o			\
	common/msg_queue.o			\
	common/permute_tx.o			\
	common/pseudorand.o			\
	common/setup.o				\
	common/type_to_string.o			\
	common/utils.o

update-mocks: $(CHANNELD_TEST_SRC:%=update-mocks/%)

$(CHANNELD_TEST_PROGRAMS): $(CCAN_OBJS) $(BITCOIN_OBJS) $(WIRE_OBJS) $(CHANNELD_TEST_COMMON_OBJS)

$(CHANNELD_TEST_OBJS): $(LIGHTNINGD_CHANNEL_HEADERS) $(LIGHTNINGD_CHANNEL_SRC)

check-units: $(CHANNELD_TEST_PROGRAMS:%=unittest/%)
