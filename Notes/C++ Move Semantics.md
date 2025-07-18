The move method in [[C++]] allows us to sort of 'move' objects/memory rather than copying memory.

		int foo(int&& i) {
			int j = i;
			++j;
			
			return j;
		}
		
		int x = 7;
		foo(std::move(x));
		
You can also use move semantics to move classes by simply implementing a move constructor as you would a copy constructor.

