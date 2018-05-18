# NMOS Identity & Timing

This is a work in progress effort to define an identity and timing model for audio, video and data. Upon completion, this model is intended to be used across the NMOS family of specifications (where applicable).

The primary focus of the activity is in the area of Sources, Flows and Grains identified within the [JT-NM Reference Architecture](http://www.jt-nm.org/RA-1.0/JT-NMReferenceArchitecturev1.0%20150904%20FINAL.pdf). It will examine their identity and timing characteristics, identifying how aspects should be constrained in order to permit interoperable implementations capable of meeting the needs of the project's user stories. Further details can be found in the [Project Proposal](ProjectProposal.pdf).

This activity will not define mappings for identity and timing data into transports (such as RTP, HTTP and others), but should be able to provide recommendations for the likely entities that would need to be carried in order to achieve the various user stories which have been proposed.

## Activity Roadmap

### 1. The Core Model

[Input material](input_material/) has been provided to bootstrap this process. The intention is to define a solid foundation using terminology which is relatively agnostic to existing work. This should define a minimal set of constructs which provide a means to refer to time related media samples using common terminology across a range of existing technologies, both within and outside the scope of Internet Protocol based systems.

### 2. The NMOS Model

Using the Core Model as a starting point, consideration will be made of the various user stories submitted to the activity, and how the concepts of Sources and Flows (and others) can help us to achieve these. These entities should then be described using terms defined by the Core Model, along with a set of constraints to make their purpose and permitted usage clear.

### 3. Implementation Considerations & Optimisations

With a model in place, we will need to ensure it is implementable and suitably optimised (or optimisable). This will likely result in advisory material for implementers of hardware and software which uses NMOS APIs and transport mappings.
