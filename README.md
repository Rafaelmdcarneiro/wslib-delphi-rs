# wslib
Delphi websocket library wrapped by Rust.

# Description
## InitWslib
   In the function, appMainBlock indicates whether to block the application of the main system. It is mainly used to start the asynchronous blocking runtime function of rust's tokio. Application.Run is used to block. When it is set to false, it will not be blocked. Therefore, if you want to set it to true, please remove Application.Run at the beginning of the application and use InitWslib instead.

## Instructions
   Since the websocket library currently used cannot support memory reuse, in order not to continue to increase unnecessary memory copy and release operations, the memory block sent can only be allocated using rust's internal allocation unit. Therefore, two structures TRustStream and TRustBuffer are implemented to obtain and operate rust's memory blocks. In addition, once the memory block is sent, it can no longer be used. Due to the ownership mechanism of rust, it is directly moved to the internal sending. After use, it will be released by itself. Therefore, after each sending, the memory structure will be automatically cleaned up. In addition, for the processing of AfterSend, this also does not need to be released. The internal structure memory of rust will be automatically released. In addition, there is a memory allocator inside rust, so its allocation and use efficiency is still good. Let's use it like this for the time being.
