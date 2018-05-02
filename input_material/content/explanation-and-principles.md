# Explanation / Principles / Approach to designing the model

* Primarily we are interested in modelling time-varying information. So, the focus is on placing information / data onto a "time line" / "time axis".
* We want an approach that can work with broadcast A/V but is not specific to it i.e. other types of data are just as important.
* We use "continuous" time (measured in seconds) only &ndash; to keep things simple we only want one "kind" of time in the model. "Continuous" time (measured in seconds) is completely universal and well understood. Its universality is important given that we wish to build highly distributed, de-coupled systems yet still be able to identify and synchronise the data produced throughout these systems.
* We want a flexible and generic model and so only define essential entities in the "core" of the model &ndash; we focus on time-varying information communicated in "concrete" form as a `TDS`.



Given all of the above, in the "core" model:

* We do not model other kinds of data such as ordered (but not timed related) sequences of data (e.g. sequences of images which will be played in the specified order but at an unknown rate).
* We do not model the different "layers" / "facets" of creating `TDS`s from a media signal (such as sampling, encoding, and byte-packing the encoded signal). These "layers" / "facets" are not universally applicable to all information, and indeed can be different even for types of broadcast A/V content.
* We do not model any relationships between entities other than those fundamental to the functioning of the "core" of the model. There are numerous relationships possible &ndash; their importance will depend on the scenario. These relationships can be added by other layers of modelling.
* We do not introduce any A/V media "restrictions". In real implementations there are many restrictions that would probably be put in place &ndash; but these should not be part of the core model, not least because they are impossible to define generically. For example, should each Data Object contain just a single media sample? (but what about video frames with two fields?) Should each `TDS` be mono-essence? (but what about colour video that is to be shown using separate RGB projectors; or multi-channel audio? &ndash; are these considered mono-essence?)


