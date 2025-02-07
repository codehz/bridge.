# Dynamic References
Dynamic references can be used to provide context sensitive data to users such as array indices, the name of the opened file or available family names.

### Lightning Cache References
Since v0.13.0-pre10 it is possible to define which file data you want to cache. This cached data can be accessed for providing more meaningful auto-completions efficiently. Stored data can be referenced inside auto-completions like this: ```$dynamic.cache.<FILE TYPE>.<CACHE KEY>```

[Read more on configuring the Lightning Cache](https://github.com/solvedDev/bridge./blob/master/plugin_docs/lightning_cache.md)

### Built-in References
| Reference | Description 
| --- | --- 
| ```$dynamic.bridge_core.is_active``` | Returns whether the bridge. Core plugin is active
| ```$dynamic.bridge_core.is_not_active``` | Returns whether the bridge.  plugin is not active
| ```$dynamic.list.next_index``` | Returns the next array index
| ```$dynamic.list.index_pair``` | Returns only "0" & "1"
| ```$dynamic.list.index_triple``` | Returns "0", "1" & "2"
| ```$dynamic.setting.target_version``` | Returns one of the target version defined under ```static/auto_completions/versions.json```
| ```$dynamic.entity.component_list``` | Returns the available component names
| ```$dynamic.entity.component_groups``` | Returns component group names inside the current file
| ```$dynamic.entity.events``` | Returns event names inside the current file
| ```$dynamic.entity.animation_references``` | Returns animation references inside the current file
| ```$dynamic.entity.all_events``` | Returns all event names
| ```$dynamic.entity.@events``` | **DEPRECATED** - Use ```('@s ' + $dynamic.entity.all_events)``` for prefixing
| ```$dynamic.recipe.pattern_keys``` | Returns pattern keys defined inside the "pattern" array
| ```$dynamic.biome.name_references``` | Returns all available biome names
| ```$dynamic.animation_controller.current_states``` | Returns currently defined states
| ```$dynamic.animation_controller_ids``` | Returns all animation controller ids
| ```$dynamic.animation_ids``` | Returns all animation ids
| ```$dynamic.client_entity.animation_references``` | Returns animation references inside the current file
| ```$dynamic.rp.item_textures``` | Returns all textures defined inside the ```item_texture.json``` file
| ```$dynamic.rp.terrain_textures``` | Returns all textures defined inside the ```terrain_texture.json``` file
| ```$dynamic.rp.entity_textures``` | Returns all files inside ```textures/entity/```
| ```$dynamic.rp.item_png``` | Returns all files inside ```textures/items/```
| ```$dynamic.rp.block_png``` | Returns all files inside ```textures/blocks/```
|  ```$dynamic.siblings``` | Returns parent context of the currently selected JSON node as JSON
|  ```$dynamic.children``` | Returns childrens of the currently selected node as JSON
|  ```$dynamic.current_file_name``` | Returns current file name
|  ```$dynamic.loot_table_files``` | Returns all loot table files
|  ```$dynamic.trade_table_files``` | Returns all trade table files
|  ```$dynamic.function_files``` | Returns all function files
