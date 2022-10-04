# Version

When an Object of the ML Registry is updated, such that its upstream Dependency Map has changed, then the Version of the Object is incremented.

\[Wording to be updated] Updating the Version vs Creating a new Object:\
If an Object can still be used in the same way by all downstream Objects (i.e. all Dependency Maps to which this Object belongs), then its version can be updated. If it is a breaking change (i.e. it will not work with current downstream Dependency Maps), then should this be handled using semantic versioning, or should a new Object be created?

What if the logic used to create a [feature](../basic-objects/feature/ "mention") changes, but it is still stored under the same name in the same [data-source.md](../storage-location/data-source.md "mention").
