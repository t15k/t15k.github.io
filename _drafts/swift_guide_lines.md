- Don't do IO operations inside iterators
  Exception is if you can do all error handling inside the
  iterator, so no exception has to go out.