lib_LTLIBRARIES = liballreduce.la libvw.la libvw_c_wrapper.la

liballreduce_la_SOURCES = allreduce.cc

bin_PROGRAMS = vw active_interactor

libvw_la_SOURCES = hash.cc global_data.cc io_buf.cc parse_regressor.cc parse_primitives.cc unique_sort.cc cache.cc rand48.cc simple_label.cc multiclass.cc oaa.cc multilabel_oaa.cc boosting.cc ect.cc autolink.cc binary.cc lrq.cc cost_sensitive.cc multilabel.cc label_dictionary.cc csoaa.cc cb.cc cb_adf.cc cb_algs.cc search.cc search_meta.cc search_sequencetask.cc search_dep_parser.cc search_hooktask.cc search_multiclasstask.cc search_entityrelationtask.cc search_graph.cc parse_example.cc scorer.cc network.cc parse_args.cc accumulate.cc gd.cc learner.cc lda_core.cc gd_mf.cc mf.cc bfgs.cc noop.cc print.cc example.cc parser.cc loss_functions.cc sender.cc nn.cc bs.cc cbify.cc topk.cc stagewise_poly.cc log_multi.cc active.cc kernel_svm.cc best_constant.cc ftrl.cc svrg.cc lrqfa.cc interact.cc comp_io.cc interactions.cc vw_exception.cc

libvw_c_wrapper_la_SOURCES = vwdll.cpp

# accumulate.cc uses all_reduce
libvw_la_LIBADD = liballreduce.la

ACLOCAL_AMFLAGS = -I acinclude.d

AM_CXXFLAGS = ${BOOST_CPPFLAGS} ${ZLIB_CPPFLAGS} ${PTHREAD_CFLAGS} -Wall -Wno-unused-local-typedef
AM_LDFLAGS = ${BOOST_LDFLAGS} ${BOOST_PROGRAM_OPTIONS_LIB} ${ZLIB_LDFLAGS} ${PTHREAD_LIBS}

CXXOPTIMIZE = -ffast-math

if PROFILE
CXXOPTIMIZE += -pg
endif

if VWBUG
CXXOPTIMIZE += -g -O1
else
CXXOPTIMIZE += -O3 -fomit-frame-pointer -fno-strict-aliasing -DNDEBUG 
endif

if NITPICK
AM_CXXFLAGS += -Wextra -Wundef -Wshadow -Wunsafe-loop-optimizations -Wconversion -Wmissing-format-attribute
AM_CXXFLAGS += -Wredundant-decls -ansi -Wmissing-noreturn
endif

if PARALLELIZE
AM_CXXFLAGS += -Wno-strict-aliasing -fopenmp
endif

if FREEBSD
AM_CXXFLAGS += -l compat
else
AM_CXXFLAGS += -pedantic
endif

if CLANG_LIBCXX
AM_CXXFLAGS += -stdlib=libc++
endif

AM_CXXFLAGS += $(CXXOPTIMIZE)

vw_SOURCES = main.cc
vw_CXXFLAGS = $(AM_CXXFLAGS)

vw_LDADD = libvw.la liballreduce.la
vw_DEPENDENCIES = libvw.la liballreduce.la

active_interactor_SOURCES = active_interactor.cc
