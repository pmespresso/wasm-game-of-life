### WASM Game Of Life

#### Notes

##### Interfacing Javascript and Rust

* JS values (Object, Arrays, DOM nodes) live on the GC'ed heap.
* Rust values live in WebAssembly's distinct linear memory space.
* **WebAssembly currently does not have direct access to the JS heap**
* **JS can read/write to the WASM linear memory space, but only as an ArrayBuffer of scalar values (u8, i32, f64, etc...)**
* WebAssembly functions receive and return scalar values.

* `wasm_bindgen` defines a standard of communication across the boundary between the JS heap and WebAssembly linear memory space. It is a tool for designing the interface chosen by the end developer.

* When designing such interface between JS and WASM, we want to minimize:
1. Copying in and out of WASM linear memory space
2. Serializing/Deserializing operations

**Rule of Thumb** -> a good JS ↔ WASM interface design is often one where large, long-lived data structures are implemented as Rust types that live in the WebAssembly linear memory, and are exposed to JavaScript as opaque handles.
