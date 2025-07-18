> The basic job of any linker or loader is simple: it binds more abstract names to more concrete names, which permits programmers to write code using the more abstract names. That is, it takes a name written by a programmer such as `getline` and binds it to ‘‘*the location 612 bytes from the beginning of the executable code in module `iosys`.*’’ 
> 
> Or it may take a more abstract numeric address such as ‘‘*the location 450 bytes beyond the beginning of the static data for this module*’’ and bind it to a numeric address.
> 
> John R. Levine in his book, '*Linkers & Loaders*'

## Key Tasks

- Program loading: Copying a program from secondary storage to main memory so it's ready to run.
- [[Relocation]]: Assigning load addresses to the parts of the program, adjusting the code and data in it to reflect the available addresses assigned by the computer (to avoid overlapping addresses).
- Symbol resolution: Resolving symbol references, i.e. if you call a routine from a library the linker notes the location assigned to that routine in the library and patches the caller's object code to it so it refers to that location.

### A Note on Overlapping Responsibilities

Programs can be linkers (symbol resolution), loaders (program loading) or both. Any of those options can do relocation.

All options patch object code, one of the few programs outside of debuggers that does this, very powerful and very easy to fuck up.

## [[Linkers]]

## Storage Allocation

The first job of any linker or loader. Shit can't be done until the necessary space has been allocated.

### Segments and Addresses

See [[Executable and Linkable Format (ELF) Files]] for a basic overview.

Every [[Object Files]] or executable file uses a model of the target address space, it's built around it, right? Usually this is the target computer's address space but sometimes it might be something like a shared [[Object Code Libraries]].

The base issue here: ***overlap***. You need to ensure all segments in a program are defined and have addresses but that those addresses don't overlap if they're not supposed to.

Naturally this is a *two-pass* process, you can't assign something unless you know the size of all segments that logically precede it. 

#### The Simple Storage Layout

Input to [[Linkers]] is a set of modules, each of which are made of a single segment starting at location 0, the largest address space also starts at 0.

Linker or loader examines each module in turn, allocating storage sequentially. Starting address of each is the **sum of the prior module lengths**. Generally a linker will round up each length to a multiple of the most stringent alignment the architecture it's on requires (4 or 8 bytes is standard baby).

#### The Many Segment Types Issue

Normally you got several kinds of segments, except for the real simple [[Object Files]] formats, *so how do you get your [[Linkers]] to group corresponding segments from all the input modules together*?

For this example, each module has some text size, data size and BSS size, ok?

As the linker reads each module it allocates space for each of the text, data and BSS parts as though each segment were *separately allocated at zero*, after it finishes reading all the input files the linker now knows the total size of each of the segments text, data and BSS. 

So what does it do next? It *fucking adds the total of the cumulative text size sections to each of the data sections and adds the total of text and data to the BSS sections*, **it's fuckin' fantastic**. Of course it rounds up each allocated size byte wise.

#### The Segment to Page Alignment Issue

If you load text and data sections into seperate memory pages the size of the text section has to be rounded up to a full page and the subsequent data and BSS sections adjusted in accordance. [[UNIX]] systems use a trick where the data is started straight after the text in the [[Object Files]], mapping the page into the file into virtual memory ([[Paging and Virtual Memory]]) twice, once read-only for the text and the second copy-on-write for the data.

This means the data addresses logically start **exactly** one page beyond the end of the text, so instead of rounding up the data addresses start exactly 4K (or whatever the page size is) beyond the end of the text.

### Linker Control Scripts

Generally for fine-grain control in messy environments, looking at you [[Embedded Systems]]. Defined in its own language. Also done via [[Command Line]] switches.

#### Example of a Linker Script

```
OUTPUT_FORMAT("coff-i386")
	SEARCH_DIR(/usr/local/lib);
ENTRY(_start)
SECTIONS
{
	.text SIZEOF_HEADERS : {
		*(.init)
		*(.text)
		*(.fini)
		etext = .;
	}
	.data 0x400000 + (. & 0xffc00fff) : {
		*(.data)
		edata = .;
	}
	.bss SIZEOF(.data) + ADDR(.data) :
	{
		*(.bss)
		*(COMMON)
		end = .;
	}
	.stab 0 (NOLOAD) :
	{
		[ .stab ]
	}
	.stabstr 0 (NOLOAD) :
	{
		[ .stabstr ]
	}
}
```

### A Note On Designing Linkers For [[Embedded Systems]]

> Linkers for embedded systems provide script languages that let the programmer define areas of the address space, and to allocate particular segments or object files into those areas, also specifying the alignment requirements for segments in each area. (*Linkers & Loaders*, John R. Levine)

[[Linkers]] for specialised processors normally have special features to support the peculiarities of that processor and these must be taken into account.

### [[Executable and Linkable Format (ELF) Files]] Storage Allocation

Generally considered more complex than a.out linking due to the set of input segments (sections in ELF terminology) being so-and-so large, they need to be turned into loadable segments (sections in ELF terminology).

The linker also needs to create the program header table for the program loader, and certain special sections needed for [[Dynamic Linking]].

Although the linking process remains about the same. But unlike a.out, ELF objects are not loaded near address zero but somewhere in the middle of the address space so the [[Stack]] can grow down below the text segment and the [[Heap]] up from the end of the data.

ELF does use the trick from [[QMAGIC]] of including the header  in the `.text` segment so the actual text segment starts are the ELF header and program table.d

## [[Symbol Management]]

See also:
- [[C++ Compilation]]
- *Linkers & Loaders* by John R. Levine