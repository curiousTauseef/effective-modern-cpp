## tasks and threads
- 2 choices for running function doAsyncWork asynchronously
	- create a std::thread and run doAsyncWork on it (thread based approach)
		- std::thread t(doAsyncWork);
	- pass doAsyncWork to std::async (task based approach)
		- auto fut = std::async(doAsyncWork);
	- prefer task based approach
- task approach
	- can retrieve return value with get function on the future
	- can retrieve exceptions thrown
	- higher level abstraction
		- no need to manage a thread
			- hardware threads are computational and one or more hardware threads are provided with each CPU core
			- software threads (OS or system threads) are managed by the operating system and mapped to hardware threads
			- std::thread are objects in a C++ process as handles to underlying software threads
				- limited # of software threads and a std::system_error exception is thrown when no more threads are available
		- standard library manages thread
			- may run async task on the current thread
				- can cause load balancing issues and lack of responsiveness on GUI threads
				- in those cases pass std::launch::async policy to std::async
					- ensures execution on separate thread
- thread approach
	- gives access to API of underlying threading implementation
		- thread priorities or affinities
		- native_handle method
- task launch policy
	- std::launch::async forces running on a separate thread
	- std::launch::deferred forces synchronous execution only when the results are needed with get or wait
	- default launch policy is either async or deferred (unknown)