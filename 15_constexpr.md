## constexpr
- conceptually const value known during compilation
	- constexpr functions need not be const nor known during compilation
- constexpr objects are const and known during compilation (translation)
	- can be placed in read-only memory
	- integral values can be used where an integral constant expression is needed
		- specification of array sizes
		- integral template arguments
		- enumerator values
		- alignment specifiers
- constexpr functions produce compile time constants when they're called with compile time constants
	- constexpr if input is constexpr
	- else a normal function (so no downside?)
	- restrictions on implementation	
		- for C++11 can not have more than a single executable return statement
			- conditional "?:" operator can be used in place of if-else
			- recursion can be used instead of loops
			- constexpr int pow(int base, int exp) noexcept { return (exp == 0? 1 : base * pow(base, exp - 1)); }
		- for C++14 restrictions are much looser
			- input output must be literal types
		- literal types are ones with values determined during complation
			- all built-in types except void (C++11)
			- user defined types can be too if constructors and other member functions are constexpr
			