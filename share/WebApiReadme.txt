---------------------
[Host Web API Server]
---------------------
You can enable Web API Server to get server status, player and game information, send chat or kick/ban player etc.
(Refer 'How to Run Dedicated Server' above for settings, like bEnableHostWebAPIServer, HostWebAPIServerPassword, HostWebAPIServerPort)

* Web API return values

        API returns Json string with following format
        <data>: contains return data
        <message>: contains simple message, or error message if API call failed
        <succeeded>: true if API call succeeded, false if failed
        <code>: 0 on success, negative value on failure

        {
                "data": {},
                "message": "",
                "succeeded": true,
                "code": 0
        }

* Web API password
        You should set 'HostWebAPIServerPassword' in DedicatedServerConfig.json
        You should pass password as parameter in each API call
        Do not use your personal password. Use random words.

        API call example

                GET /player/count/?password=your_password
                POST /player/kick/?password=your_password&unique_id=player_unique_id

* Web API List

        POST /chat
        parameters
                message (required. chat message)
                type (optional. set chat type "announce" or "message". defaults to "announce".)
                color (optional. override text color(ex FF00FF) when type is "message". defaults to white.)
        return example
                "data": {},
                "message": "message sent",
                "succeeded": true,
                "code": 0

        GET /player/count
        return example
                "data": { "num_players": 2 }

        GET /player/list
        return example
                "data": {
                        "0": {
                                "name": "jake",
                                "unique_id": "A1B2C3D4",
                                "character_guid": "E5F6G7H8",
                                "location": "X=2590.089 Y=1682.984 Z=98.927",
                                "vehicle":
                                {
                                        "name": "Scooty",
                                        "unique_id": 175114
                                }
                        },
                        "1": {
                                "name": "dooli",
                                "unique_id": "A1B2C3D5",
                                "character_guid": "E5F6G7H9",
                                "location": "X=-108.632 Y=463.258 Z=188.150"
                        }
                }

        POST /player/kick
        parameters
                unique_id (required. player's unique_id from player/list)

        GET /player/banlist
        return example
                "data": {
                        "0": {
                                "name": "banned_user",
                                "unique_id": "B9C8D7E6",
                                "reason": "Toxic behavior",
                                "left_time_seconds": 86400
                                }
                        }

        POST /player/ban
        parameters
                unique_id (required. player's unique_id from player/list)
                hours (optional. number of hours to ban for. default is permanent.)
                reason (optional. reason for ban.)

        POST /player/unban
        parameters
                unique_id (required. player's unique_id from player/banlist)

        GET /player/role/list
        parameters
                role (required. set player role 'admin' or 'police'.)
        return example
                "data":{
            "admin":
            {
                "0":
                {
                    "unique_id": "A1B2C3D4",
                    "nickname": "jake"
                },
                "1":
                {
                    "unique_id": "B9C8D7E6",
                    "nickname": "betty"
                }
            }
                }

        POST /player/role/add
        parameters
                role (required. set player role 'admin' or 'police'.)
                unique_id (required. player's unique_id from player/list)

        POST /player/role/remove
        parameters
                role (required. set player role 'admin' or 'police'.)
                unique_id (required. player's unique_id from player/list)

        GET /delivery/sites
        return example
                "data": {
                        "17":
                        {
                                 "guid": "A1B2C3D44ABD6FBBB130BC953C85E1BD",
                                 "name": "Construction Site",
                                 "location": "X=-3350.465 Y=2.171 Z=100.000",
                                 "Deliveries":
                                 {
                                          "0":
                                          {
                                                        "id": 68,
                                                        "cargo_type": "Sand",
                                                        "num_cargos": "1/1",
                                                        "sender_point": "A1B2C3D44ABD6FBBB130BC953C85E1BD",
                                                        "receiver_point": "2F3A8E4C4CB0A3A1273B8A8036FCDBCA",
                                                        "register_time": 122.30276489257812,
                                                        "expire_time": 482.48467864096165,
                                                        "base_payment": 5,
                                                        "timer_seconds": -1
                                          }
                                 },
                                 "InputInventory":
                                 {
                                          "0":
                                          {
                                                        "amount": 0,
                                                        "cargo":
                                                        {
                                                                 "cargo_key": "CARROT_KEY",
                                                                 "name": "Carrots",
                                                                 "type": "Box",
                                                                 "space_types": "Flatbed, Box",
                                                                 "volume_size": 1,
                                                                 "weight_range": "X=0.000 Y=0.000",
                                                                 "allow_stacking": "false",
                                                                 "use_damage": "false",
                                                                 "fragile": 0,
                                                                 "spawn_probability": 10,
                                                                 "num_cargo_range": "X=1 Y=2",
                                                                 "base_payment": 0,
                                                                 "payment_per1km": 220,
                                                                 "delivery_distance_range": "X=0 Y=0"
                                                        }
                                          }
                                 },
                                 "OutputInventory":
                                 {
                                          "0":
                                          {
                                                        "amount": 1,
                                                        "cargo":
                                                        {
                                                                 "cargo_key": "SAND_KEY",
                                                                 "name": "Sand",
                                                                 "type": "Sand",
                                                                 "space_types": "Dump",
                                                                 "volume_size": 1,
                                                                 "weight_range": "X=1600.000 Y=1600.000",
                                                                 "allow_stacking": "false",
                                                                 "use_damage": "false",
                                                                 "fragile": 0,
                                                                 "spawn_probability": 10,
                                                                 "num_cargo_range": "X=5 Y=20",
                                                                 "base_payment": 0,
                                                                 "payment_per1km": 380,
                                                                 "delivery_distance_range": "X=0 Y=0"
                                                        }
                                          }
                                 }
                        }
          }

        GET /town/list
        return example
                "data": {
                        "towns": [
                                {
                                        "name": "Downtown",
                                        "population_bonus": "12.50%",
                                        "production_bonus": "5.00%",
                                        "payment_bonus": "3.25%"
                                },
                                {
                                        "name": "Harbor District",
                                        "population_bonus": "0.00%",
                                        "production_bonus": "0.00%",
                                        "payment_bonus": "0.00%"
                                }
                        ]
                }

        GET /company/list
        return example
                "data": {
                        "companies": [
                                {
                                        "guid": "A1B2C3D44ABD6FBBB130BC953C85E1BD",
                                        "name": "Motor Town Express",
                                        "desc": "We deliver anywhere.",
                                        "owner": "jake",
                                        "num_players": 2,
                                        "players": [
                                                {
                                                        "unique_id": "A1B2C3D4",
                                                        "character_guid": "E5F6G7H8",
                                                        "character_name": "jake"
                                                },
                                                {
                                                        "unique_id": "A1B2C3D5",
                                                        "character_guid": "E5F6G7H9",
                                                        "character_name": "dooli"
                                                }
                                        ],
                                        "num_vehicles": 1,
                                        "vehicles": [
                                                {
                                                        "vehicle_id": 175114,
                                                        "vehicle_name": "Scooty"
                                                }
                                        ],
                                        "is_corporation": false
                                }
                        ]
                }

        GET /company/profit
        parameters
                guid (required. company guid from company/list)
                days (required. number of recent days to return. clamped to the server's max daily stat count.)
        return example
                "data": {
                        "guid": "A1B2C3D44ABD6FBBB130BC953C85E1BD",
                        "name": "Motor Town Express",
                        "days": 3,
                        "stats": [
                                {
                                        "days_ago": 0,
                                        "total_income": 12500,
                                        "total_cost": 4300,
                                        "depot_stats": [
                                                {
                                                        "building_guid": "2F3A8E4C4CB0A3A1273B8A8036FCDBCA",
                                                        "total_cost": 2100
                                                }
                                        ]
                                },
                                {
                                        "days_ago": 1,
                                        "total_income": 9800,
                                        "total_cost": 3700,
                                        "depot_stats": []
                                },
                                {
                                        "days_ago": 2,
                                        "total_income": 0,
                                        "total_cost": 0,
                                        "depot_stats": []
                                }
                        ]
                }

        GET /fire/list
        return example
                "data": {
                        "num_fires": 1,
                        "fires": [
                                {
                                        "fire_id": 42,
                                        "location": "X=1200.000 Y=-340.500 Z=98.927",
                                        "num_cells": 6,
                                        "fire_radius": 450.0,
                                        "spotted": true,
                                        "predicted_duration_seconds": 180.0,
                                        "extinguish_started": false,
                                        "num_extinguishing_players": 1,
                                        "extinguishing_players": [
                                                {
                                                        "unique_id": "A1B2C3D4",
                                                        "character_guid": "E5F6G7H8",
                                                        "character_name": "jake"
                                                }
                                        ]
                                }
                        ]
                }

        GET /version
        return example
                "data": { "version": "0.7.13+CT4(B804)" }

        GET /housing/list
        return example
                "data":{
                        "HousingTest_House0": {
                                "owner_unique_id": "A1B2C3D4",
                                "expire_time": "2025.04.11-03.04.57 (+6 days 23 hours)"
                        }
                }
