## Introduction

My design models a gaming system where elements can appear multiple times, these elements include inventory items, enemy loot drops, resource system, and monster spawn tables. Rather than going with a traditional Set that restricts elements to a single occurrence it's better to implement a MultiSet, which allows elements to appear multiple times. By storing strings that represent names of items and associating each with a count to represent exactly how many copies exist within a collection. For this design I'm building it atop a Sequence(<string>). 

## Design Philosophy

The design of this will prioritize efficiency, simplicity, extensibility, and readability.

**Efficiency** for this design is focusing on the practical suitability for realistic gameplay workloads. Choosing to build atop Sequence data structure it'll benefit predictable performances, memory simplicity, and low structural overhead. Actions such as searching for an item, counting how many times it appears, or removes requires scanning through a list. Keeping in mind that a majority of game inventories and resource pools are mainly small, at such a scale a linear scan typically completes very quickly. Building atop a Sequence(<string>) data structure it stores its elements contiguously in memory making it cache-friendly and predictable. 

**Simplicity** allows operations in the Sequence(<string>) data structure to behave in an easily understood manner. Making the operations built atop are straightforward and concise making it easy to add any future modifications. Since there is not another indexing system because each occurrence of an item is stored in the list and the internal state just mirrors what the MultiSet represents makes it simple to test and debug. Meaning if a problem were to happen I can examine the list directly, giving it a level of transparency.

**Extensibility** ensures that the Sequence(<string>) data structure can evolve/grow as game features or operations grow to become more complex over time. With building atop Sequence(<string>) data structure there are minimal constraints ensuring that there is room to easily add new behaviors, traversal patterns, etc. Items will have the ability to be dynamically inserted, rearranged, duplicated, or removed without breaking the structural constraints. 

**Readability** is essential in the design for the MultiSet because it'll make sure the public interface remains clear and understandable, along with the internal state. By building atop a Sequence(<string>) data structure avoids complex data structures and keeps it simple, like a bag of elements, for developers. This level of transparency helps testing and debugging become more readable. This will also help with the long-term stability.

The clients for the MultiSet class would be the inventory, crafting, loot system, monster spawning, and resource tracker. The inventory would keep track of what items are being collected by the player. While the crafting checks and uses the material items from the player. The loot system would randomly decide what items get dropped by defeated monsters, and what items if any are in chests. The monster spawning dictates which monster would spawn by weight, difficulty that is determined by weight, and what areas certain monsters have a better chance of spawning than others. Lastly the resource tracker would determine the quantities of items in the environment. All these systems would call operations like 
* add(item)
* remove(item)
* count(item)
* merger(other)

Meanwhile the user side that has access to the MultiSet class is me, and any collaborating developers working on the systems to interact with the MultiSet.

## Core Operations
