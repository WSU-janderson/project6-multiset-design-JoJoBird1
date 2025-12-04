## Introduction

My design models a gaming system where elements can appear multiple times, these elements include inventory items, enemy loot drops, resource system, and monster spawn tables. Rather than going with a traditional Set that restricts elements to a single occurrence it's better to implement a MultiSet, which allows elements to appear multiple times. By storing strings that represent names of items and associating each with a count to represent exactly how many copies exist within a collection. For this design I'm building it atop a Sequence(<string>). 

## Design Philosophy

The design of this will prioritize efficiency, simplicity, extensibility, and readability.

**Efficiency** for this design is focusing on the practical suitability for realistic gameplay workloads. Choosing to build atop Sequence data structure it'll benefit predictable performances, memory simplicity, and low structural overhead. Actions such as searching for an item, counting how many times it appears, or removes requires scanning through a list. Keeping in mind that a majority of game inventories and resource pools are mainly small, at such a scale a linear scan typically completes very quickly. Building atop a Sequence(<string>) data structure it stores its elements contiguously in memory making it cache-friendly and predictable. 

**Simplicity** allows operations in the Sequence(<string>) data structure to behave in an easily understood manner. Making the operations built atop are straightforward and concise making it easy to add any future modifications. Since there is not another indexing system because each occurrence of an item is stored in the list and the internal state just mirrors what the MultiSet represents makes it simple to test and debug. Meaning if a problem were to happen I can examine the list directly, giving it a level of transparency.

**Extensibility** ensures that the Sequence(<string>) data structure can evolve/grow as game features or operations grow to become more complex over time. With building atop Sequence(<string>) data structure there are minimal constraints ensuring that there is room to easily add new behaviors, traversal patterns, etc. Items will have the ability to be dynamically inserted, rearranged, duplicated, or removed without breaking the structural constraints. 

**Readability** 