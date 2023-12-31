---
layout: default
title: State Api
parent: Celin.State
grand_parent: Modules
nav_order: 2
---

# Api

Most of `Celin.State` functionality is provided as an `Api` on the state variable, returned by the `New-Celin.State` or `Use-Celin.State` Cmdlets.

```powershell
# Create a new state and return state variable
$var = New-Celin.State test a, b, c
# Get a variable to an existing state
$test = Use-Celin.State test
# The state value is an Hashtable with current state value
$test
```

##### [PSObject] this[string member]

Member accessor.

```powershell
# Set the value of member "a"
# Members are case sensitive and must be enclosed in quotes!
$var["a"] = "This is a Value"
# Get the value of member "a"
$var["a"]
# Using the Set-Celin.State cmdlet Alias cstate
# can make the script more readable.
cstate a "A Set with cstate"
"Pipe A" | cstate a
# And using the state variable dot syntax
# to read members
$var.a
```

##### [Hashtable] _SetLabel_ (string label, bool clear = false, bool force = false)

Sets the label name on the current state.

```powershell
# Label the state, set all members to null and
# force override any existing label of same name.
# The 'done' variable holds the labelled state value.
$done = $var.setLabel("done", $true, $true)
```

##### _Undo()_

Deletes that latest state, making current state the previous.

```powershell
$var.undo()
```

##### [string] _Name_

Returns the state's name.

```powershell
# Display the state's name
"The State's name is $($var.name)"
```

##### [bool] _Tracing_

Returns `true` if state flagged with `Trace`. 

```powershell
# Write if the state is tracing
"The $($var.name) state is$($var.tracing ? $null : ' NOT') tracing!"
```

##### [PSCustomObject[]] Trace

Returns the state as an array of `PSCustomObject` with all the member values as strings (using `ToString()`).

```powershell
# Display the trace
$var.trace
```

##### [Hashtable[]] _Labels_

Returns an array of labels as `Hashtable` in __Reverse__ order.  The label uses '#' as membe name (uses # inside quotation marks when referenced).

```powershell
# Display Labels
$var.labels
# Display the last Label set
$var.labels[0]
# Display the first Label set
$var.labels[$var.labels.length - 1]
```

##### [Hashtable[]] _Values_

Returns the current states values as `Hashtable` in __Reverse__ order.

```powershell
# Display Values
$var.values
# Display Current Values (same as $var)
$var.values[0]
# Display Previous Values
$var.values[1]
```

##### [List<StateValue>] _States_

Returns the state as a list of `StateValue` type, which is the native type.

```powershell
# Display state
$var.states
```
