CLEANEXTS   = o so

CXX = $(RASPBIANCROSS)g++

SRC = tflite/custom_op.cc tflite/edgetpu_context_direct.cc tflite/custom_op_data.cc tflite/edgetpu_context_factory.cc \
     tflite/custom_op_direct.cc	tflite/edgetpu_delegate_for_custom_op.cc tflite/custom_op_user_data_direct.cc \
     tflite/edgetpu_delegate_for_custom_op_tflite_plugin.cc tflite/edgetpu_c.cc	tflite/edgetpu_manager_direct.cc \
     api/allocated_buffer.cc api/buffer.cc api/driver_factory.cc api/driver_options_helper.cc \
     api/layer_information.cc api/tensor_util.cc api/watchdog.cc \
     driver/aligned_allocator.cc driver/allocator.cc driver/device_buffer.cc driver/device_buffer_mapper.cc \
     driver/dma_chunker.cc driver/dma_info.cc driver/dma_info_extractor.cc driver/driver.cc driver/driver_factory.cc \
     driver/driver_factory_default.cc  \
     driver/executable_util.cc driver/instruction_buffers.cc driver/mmio_driver.cc \
     driver/package_registry.cc driver/package_verifier.cc driver/real_time_dma_scheduler.cc driver/request.cc \
     driver/run_controller.cc driver/scalar_core_controller.cc driver/single_queue_dma_scheduler.cc \
     driver/single_tpu_request.cc \
     driver/interrupt/grouped_interrupt_controller.cc driver/interrupt/interrupt_controller.cc \
     driver/interrupt/top_level_interrupt_manager.cc driver/interrupt/wire_interrupt_handler.cc \
     driver_shared/time_stamper/driver_time_stamper.cc \
     port/blocking_counter.cc port/posix_time.cc port/shared_mutex.cc port/timer_portable.cc \
     port/default/builddata.cc port/default/status_macros.cc port/default/stringprintf.cc \
     port/default/port_from_tf/logging.cc port/default/port_from_tf/status.cc port/default/port_from_tf/statusor.cc \
     driver/beagle/beagle_kernel_top_level_handler.cc driver/beagle/beagle_pci_driver_provider.cc \
     driver/beagle/beagle_pci_driver_provider_linux.cc driver/beagle/beagle_top_level_handler.cc \
     driver/beagle/beagle_top_level_interrupt_manager.cc driver/beagle/beagle_usb_driver_provider.cc


OBJ = $(SRC:.cc=.o)
DEP = $(OBJ:.o=.d)

OUTPUTFILE  = libedgetpu_direct.so
INSTALLDIR  = ../binaries

INCLUDES = \
	-I. \
	-I$(TFLOWSDK) \
	-I$(TFLOWSDK)/build/flatbuffers/include\
    -I$(TFLOWSDK)/build/abseil-cpp/
CFLAGS += $(INCLUDES) -DBUILD_EMBED_LABEL='"TENSORFLOW_COMMIT=855c4c0ee34257b98ce2d01121940efb5423a059"'

LDFLAGS = -L$(TFLOWSDK)/build/_deps/abseil-cpp-build/absl/strings \
    -L$(TFLOWSDK)/build/_deps/abseil-cpp-build/absl/flags \
    -L$(TFLOWSDK)/build/_deps/abseil-cpp-build/absl/container \
    -L$(TFLOWSDK)/build/_deps/abseil-cpp-build/absl/hash \
    -L$(TFLOWSDK)/build/_deps/abseil-cpp-build/absl/base \
    -L$(TFLOWSDK)/build/_deps/abseil-cpp-build/absl/numeric \
    -L$(TFLOWSDK)/build/_deps/abseil-cpp-build/absl/types \
    -Wl,--whole-archive -labsl_str_format_internal -labsl_flags_marshalling -labsl_strings -labsl_strings_internal\
    -labsl_bad_optional_access -labsl_raw_hash_set -labsl_hash -labsl_wyhash -labsl_city -labsl_throw_delegate \
    -labsl_int128 -labsl_raw_logging_internal -Wl,--no-whole-archive

.cc.o:
	$(CXX) $(CFLAGS) $(DEPFLAGS) $(INCLUDES) -c $< -o $@

.PHONY: all
all: $(OUTPUTFILE)

$(OUTPUTFILE): $(OBJ)
	$(CXX) -shared -fPIC $(LDFLAGS) -o $@ $^

$(DEP):

-include $(DEP)
