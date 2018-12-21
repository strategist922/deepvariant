# The workspace name appears at the top of the runfiles tree,
# and in paths to tests, so to keep python happy it is best
# if it is unique.
workspace(name = "com_google_deepvariant")

# Note: absl_py and com_google_absl (the Python and C++ abseil libraries) are
# provided by TensorFlow.

# CCTZ (Time-zone framework).
# redacted
# work in bazel, so we need to include this to enable nucleus's use of
# //absl/{time,synchronization}
http_archive(
    name = "com_googlesource_code_cctz",
    urls = ["https://github.com/google/cctz/archive/master.zip"],
    strip_prefix = "cctz-master",
)

new_http_archive(
    name = "htslib",
    build_file = "third_party/htslib.BUILD",
    sha256 = "c4d3ae84014f8a80f5011521f391e917bc3b4f6ebd78e97f238472e95849ec14",
    strip_prefix = "htslib-1.9",
    urls = [
        "https://github.com/samtools/htslib/archive/1.9.zip"
    ],
)

new_http_archive(
    name = "libssw",
    build_file = "third_party/libssw.BUILD",
    sha256 = "10b9305e5a580ee5319f736d3581916f6c873ef4475bd0c0e564c2934334732c",
    strip_prefix = "Complete-Striped-Smith-Waterman-Library-1.0",
    urls = [
        "https://github.com/mengyao/Complete-Striped-Smith-Waterman-Library/archive/v1.0.tar.gz",
    ],
)

# Import tensorflow.  Note path.
local_repository(
    name = "org_tensorflow",
    path = "../tensorflow",
)

# Required boilerplate for tf_workspace(), apparently.
# This is copied from https://github.com/tensorflow/tensorflow/blob/master/WORKSPACE
# Note: This may need to be changed if we change the tensorflow branch that we
# build against.
http_archive(
    name = "io_bazel_rules_closure",
    sha256 = "a38539c5b5c358548e75b44141b4ab637bba7c4dc02b46b1f62a96d6433f56ae",
    strip_prefix = "rules_closure-dbb96841cc0a5fb2664c37822803b06dab20c7d1",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_closure/archive/dbb96841cc0a5fb2664c37822803b06dab20c7d1.tar.gz",
        "https://github.com/bazelbuild/rules_closure/archive/dbb96841cc0a5fb2664c37822803b06dab20c7d1.tar.gz",  # 2018-04-13
    ],
)

# We need a protobuf version at this hash or later because we need the API
# introduced in
# https://github.com/google/protobuf/pull/4698 with bug fixes at
# 4725, 4835, and 4836.
# We also need our own BUILD file to support ProtoPtr optimizations.
new_http_archive(
    name = "protobuf_archive",
    build_file = "third_party/protobuf.BUILD",
    sha256 = "ab811441e16acd6e6d19abb9fd266b0acbd7c14be331de9da7f0bdb3683ae39f",
    strip_prefix = "protobuf-79700b56b99fa5c8c22ddef78e6c9557ff711379",
    urls = [
        # redacted
        # "https://mirror.bazel.build/github.com/google/protobuf/archive/a0e82dbe569552ac848d088391b63aaa1108d1a3.tar.gz",
        "https://github.com/google/protobuf/archive/79700b56b99fa5c8c22ddef78e6c9557ff711379.tar.gz",
    ],
)

# bazel_skylib is now a required dependency of protobuf_archive.
http_archive(
    name = "bazel_skylib",
    sha256 = "bbccf674aa441c266df9894182d80de104cabd19be98be002f6d478aaa31574d",
    strip_prefix = "bazel-skylib-2169ae1c374aab4a09aa90e65efe1a3aad4e279b",
    urls = ["https://github.com/bazelbuild/bazel-skylib/archive/2169ae1c374aab4a09aa90e65efe1a3aad4e279b.tar.gz"],
)

# Import all of the tensorflow dependencies.
load("@org_tensorflow//tensorflow:workspace.bzl", "tf_workspace")

tf_workspace(tf_repo_name = "org_tensorflow")

# Pull in slim.
# slim is  located inside the tensorflow/models repository.
# The slim subdirectory in the tensorflow/models repository has its own
# WORKSPACE file so we need to strip a prefix to make it the root of the
# repository.
# The prefix is "models-<commit>/slim"
# where commit is the full commit.
# Pin to the lastest version that builds for now. See b/68431494#comment4.
http_archive(
    name = "org_tensorflow_slim",
    strip_prefix = "models-6d140f139cf02ceb87afa76024c4b502a556a3e5/slim",
    urls = ["https://github.com/tensorflow/models/archive/6d140f1.tar.gz"],
)

new_local_repository(
    name = "clif",
    build_file = "third_party/clif.BUILD",
    path = "/usr/local",
)
