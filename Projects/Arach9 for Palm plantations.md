# Subproblems
- Accurate fruit detection (Multisensor, Ethanol detection, RGBD)
- 
Traversing plantation:
- Ground traversal:
	- Navigation grass, debris, ditches
- Climbing up trees:
	- Rock climbing ledge identification for palm tree stalks
	- Stuck minimization + self-rescue
	- Glide minimization by maintaining a slant to let gravity and friction do the work
- Climbing down palm trees:
	- Jumping and dampening fall with glide
- Charging via solar panels
- Suspending on palm trees:
	- Identifying stable branches

Detection:
- Fruit detection
- Ripeness assessment

Harvesting:
	- identifying cut points
	- cut mechanics
	- pushing fruit off tree?

Communication:
Mesh network to exchange:
- Localization information (GPS, SLAM, Cell tower)
- Global map reconstruction
- mission status and updates
- node status and u opdates
Robust, adaptive mesh topology:
- Node with strongest outside signal becomes root