# Extension &ndash; Grouping

Grouping is about collecting a set of entities in the model and giving it an identity. The `Source` is a form of grouping that collects a set of `Flow`s that share the properties defined by the `Source`. The grouping in this section is more about grouping entities that have a common purpose and are intended to be used together.

Some common examples of grouping are:
* Grouping `Source`s or `Flow`s that share a `Time Context` and are therefore synchronised. For example, an audio, video and subtitle group which constitutes a TV programme.
* Grouping of ISOs or sets of time-coincident audio assets related to a recording session.
* Grouping of tracks that make up a media file.

There are a number of aspects that need to be considered when defining a group and its members, such as:
* Define a group identifier that is unique.
* Define a locally unique label for each member of the group. This label along with the group identifier is used to refer to a group member.
* Define how a group member references the entity it represents. For example, by using a `Source` ID to refer to a `Source`, or a track index to refer to a track in a media file.
* Define whether the group members are ordered or not.
* Define how the group relates to entities such as `Source` and `Flow`. For example, if a group defines the members of a multi-channel audio `Source` then it is necessary to define how and when the group is used when recording an ancestry relationship for this content.

