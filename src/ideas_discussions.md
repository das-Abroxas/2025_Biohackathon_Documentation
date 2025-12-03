
# Ideas / Discussions

### How to handle RO-Crates with extremely large datasets and which integrate the complete metadata?

- Some kind of 'pagination' needed as the RO-Crate metadata file can grow extremely large
- RO-Crate specification already defines the creation and referencing of subcrates
- Problem with referencing of top-level crates from subcrates as they are not aware that they exist
  - If you describe a ßdata entity in a RO-Crate file it also has to be referenced in the `hasPart` property which would not be correct
  - Maybe just use the `isPartOf` property to reference the parent RO-Crate (only @id can be written in the `isPartOf` property which is somewhat limiting)

### How to integrate content consistency checks in File metadata?

- It would be nice to have some property shipped with the data entities of a RO-Crate that can be used to validate the data entity content integrity
- Create a custom `data integrity profile` which is referenced at the `@context` part is most likely overkill
- Just reference the following terms in the `@context` and use them with each data entity:
  - https://spdx.org/rdf/terms/#Checksum
  - https://spdx.org/rdf/terms/#ChecksumAlgorithm
  - https://spdx.org/rdf/terms/#checksumValue

- Which checksum algorithm would be best to use? Suggestions:
  - BLAKE3
  - https://sum.iscc.codes/#technical-innovation

- A problem which is still discussed is how to efficiently update the checksum value if the data entity content changes (especially for complete datasets)


### How to pass metadata updates in top level crate to referenced "subcrates"?

- Not entirely discussed to a final conclusion


### How to handle property conflicts in nested RO-Crates?

- Consolidating nested RO-Crates into a single comprehensive file would be more convenient for a user than to have the full resolved subcrates just "imported" in the main RO-Crate metadata file
- A little bit contrary to the idea of RO-Crates being self-contained

- Merging nested RO-Crates into a single comprehensive one carries the risk for conflicting definitions of entities
- Proposed merging strategies:
  - Last update overwrites -> Very simple approach but maybe leads to data loss
  - Conflicting defintions creates separate entitites -> Bloats the metadata file and adds ambiguity
  - Conflicting properties are added as duplicates into the entity -> Creates invalid JSON

- Every strategy seems to have its drawback
