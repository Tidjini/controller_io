# Controller IO

The control application has a goal to pull information from both sides and push updates for both sides. If there is connection between both sides, collect information in collections called instances and wait for the END Collection Message from the pusher side (with timeout).
wait for 0.5 of a second for the other side if there is any update. Then after the END message and the waiting time, the controller pushes instances to both sides.

If in waiting time comes an instance with the same entity and identity, that means there is a conflict, we must inform the MASTER side of it.

If the connection is lost from one side the controller must wait for END Message from this side after connectivity, before sending changes to this side, to handle conflict.

Instance / Conflict table for the controller.
instance : entity, id, values without system values (creation date, and so on), from ’MASTER’ to: ‘\*’ //all or specific name or just from, values as dictionary.

conflict has an entity, id with details of both sides.
If changes are determined in conflict, keep sending the conflict message and do not update.

After a while, set log files for instances, and conflicts and clean the controller database, at a specific time (the non working time).
