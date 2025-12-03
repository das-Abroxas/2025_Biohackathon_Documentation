# Results

---

## Extensions to ro-crate-py

```
[...] traversing the graph from the top crate to a subcrate, as suggested in the 1.2 spec.

I am proposing a simple approach here, with a new Subcrate class extending the Dataset class.
I defined this class in the main rocrate.py file, in models.py it would cause circular dependencies.

This would allow things like

main_crate = ROCrate(test_data_dir / "crate_with_subcrate")
subcrate = main_crate.get("subcrate")
subfile = subcrate.get("subfile.txt")
# or 
subfile = subcrate["hasPart"][0]

(see added tests too)

at this point I am mostly interested to know if you think that could be a viable approach before going further.

The implementation is such that the subcrate is only loaded when accessing some of its attribute, to avoid potentially loading large amount of metadata, as one purpose of the subcrate is also to reduce the amount of information in the main crate.
```

[Link to the pull request with the feature implementations](https://github.com/ResearchObject/ro-crate-py/pull/244)

---

## Extensions to ro-crate-rs

- Interactive CLI mode for RO-Crate (attached and detached) exploration and traversal

![CLI displays full loaded RO-Crate content](assets/cli_screenshot_01.png)

![CLI displays full loaded RO-Crate content](assets/cli_screenshot_02.png)


- Fulltext search index over all included entities of a RO-Crate metadata file

**Screenshot Sebastian**


- Discussion with one of the official RO-Crate specification maintainers to move the library into the official `ResearchObject` Github organization


---

## Demonstrator

- Small Webapp MVP

- Demonstrates the exploration and traversal of detached and nested RO-Crates via a file tree display
  - Can be entered with a URL pointing to a remote RO-Crate (metadata file) or uploaded as .zip file or just as RO-Crate metadata file in detached format

- Provides Preview of linked data e.g. Properties 

- Provides filter options by entity type

- Screenshots and process schema