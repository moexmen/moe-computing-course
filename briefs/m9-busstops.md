# Bus Stop Missions

## Concepts
- List processing: `map`, `filter`, `accumulate`.
- Data Abstraction: don't break the barrier.
- Data Types: be sure of input/output types of functions.

## Data Files

`bus_stops.txt`: BusStopCode, StreetName, StopDescription
```
01012,Victoria St,Hotel Grand Pacific
01013,Victoria St,St. Joseph's Ch
01019,Victoria St,Bras Basah Cplx
01029,Nth Bridge Rd,Cosmic Insurance Bldg
```

`smrt_routes.txt`: BusServiceNumber, RouteNumber, StopSequence, BusStopCode

```
106,1,1,43009
106,1,2,43179
106,1,3,43189
106,1,4,43619
106,1,5,43629
...
106,2,50,43171
106,2,51,43009
171,1,1,59009
171,1,2,59141
171,1,3,59111
171,1,4,57089
...
```

## ADTs

### Bus Stop ADT

```python
>>> bookland = make_bus_stop("01012", "Victoria St", "Bras Basah Cplx")
# Concrete implementation uses a tuple, but it can be anything:
# ("01012", "Victoria St", "Bras Basah Cplx")
>>> get_code(bookland)
"01012"
>>> get_road_name(bookland)
"Victoria St"
>>> get_description(bookland)
"Bras Basah Cplx"
```

All 4 methods are given to you.

### Methods for Tuples of Bus Stops

```python
>>> tuple_of_stops = read_bus_stop_data('bus_stops.txt')
# Returns a tuple of Bus Stop ADTs, must use make_bus_stop
>>> lookup_bus_stop_by_code(tuple_of_stops, "01012")
# Returns a Bus Stop ADT, must use get_code
>>> lookup_bus_stop_by_road(tuple_of_stops, "Victoria St")
# Returns a tuple of Bus Stop ADTs, must use get_road_name
```

All 3 methods are given to you, but you are to rewrite `lookup_bus_stop_by_road` using `filter`.

### Bus Service ADT

#### Version 1
Interface:
```python
# Assume that bus_106_raw_data has been prepared for you.
>>> bus_106_data
(('106', '1', '1', '43009'),
 ('106', '1', '2', '43179'), ...
 ('106', '2', '1', '03239'),
 ('106', '2', '2', '03211'), ... )

>>> bus_106 = make_service(bus_106_data, "106") # String!
# Returns a Bus Service ADT
>>> get_service_code(bus_106)
"106"
>>> get_route(bus_106, "2")
('03239', '03211', 'E0321', ...) # Returns tuple of BusStopCodes
```

Implementation: How a Bus Service ADT actually looks like in Python

```python
>>> print_tuple(bus_106) # Helper method is given to you
( '106',
  ( ( '43009',
      '43179',
      ...
      '03218',
      '03219'),
    ( '03239',
      '03211',
      ...
      '43171',
      '43009')))
```

Version 1 of `make_service` is given to you. You are to write `get_service_code` and `get_route`.

##### Quiz

What is wrong and how to fix?

```python
def number_of_stops_in_second_direction(bus_service):
  return len(bus_service[1][1])
```

#### Version 2

Difference: Allow names to be given to each route.

```python
>>> print_tuple(bus_106_v2)
( '106',
  ('A', 'B'),
  ( ( '43009',
      '43179',
      ...
      '03218',
      '03219'),
    ( '03239',
      '03211',
      'E0321',
      ...
      '43171',
      '43009')))
```

Changes to the interface:

```python
# new accessor method
>>> get_directions(bus_106_v2)
('A', 'B')

# get_route needs to be updated to accept non-integer route name
>>> get_route(bus_106_v2, "B")
('03239', '03211', 'E0321', ...)
```

Tasks:
1. Modify `make_service`
1. Write the new method `get_directions`
1. Update `get_route`

Observe that `get_route` is part of the abstraction barrier because it prevents changes from propagating further.

#### Two ways to generate Bus Service data to create Bus Service ADTs

How to obtain `bus_106_data` from the data file?

```python
>>> all_route_data = read_route_data('smrt_routes.txt')
(('106', '1', '1', '43009'),
 ('106', '1', '2', '43179'),
 ...
 ('106', '2', '51', '43009'),
 ('171', '1', '2', '59141'),
 ...)

# Way 1
>>> filter_routes(all_route_data, '106')
(('106', '1', '1', '43009'),
 ('106', '1', '2', '43179'),
 ...
 ('106', '2', '51', '43009'))

# Way 2
>>> split_route_data = split_routes(all_route_data)
((’171’, ((’171’, ’1’, ’1’, ’59009’), ... , (’171’, ’2’, ’73’, ’59009’))),
 (’106’, ((’106’, ’1’, ’1’, ’43009’), ... , (’106’, ’2’, ’51’, ’43009’))),
 (’184’, ((’184’, ’1’, ’1’, ’45009’), ... , (’184’, ’1’, ’52’, ’45009’))))
>>> make_services(split_route_data)
# Returns a tuple of Bus Service ADTs, uses make_service (singular) internally
```

Tasks:
- Write `read_route_data` using `map`. Can refer to `read_bus_stop_data`.
- Write `split_routes` and `make_services`.

##### Quiz Solution

```python
def number_of_stops_in_second_direction(bus_service):
  return len(get_route("2"))
```
