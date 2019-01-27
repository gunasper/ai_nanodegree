This code isn't working but I coudn't figure out why. All tests (1-31) worked. Only tests 32-35 have failed.

```
def h_setlevel(self):
    """ Calculate the set level heuristic for the planning graph

    The set level of a planning graph is the first level where all goals
    appear such that no pair of goal literals are mutex in the last
    layer of the planning graph.

    Hints
    -----
      (1) See the pseudocode folder for help on a simple implementation
      (2) You can implement this function more efficiently if you expand
          the graph one level at a time until you find the set level rather
          than filling the whole graph at the start.

    See Also
    --------
    Russell-Norvig 10.3.1 (3rd Edition)

    Notes
    -----
    WARNING: you should expect long runtimes using this heuristic on complex problems
    pseudocode:
    function SetLevel(graph) returns a value
         inputs:
          graph, an initialized (unleveled) planning graph

         graph.fill() /* fill the planning graph until it levels off */
         for layeri in graph.literalLayers do
          allGoalsMet <- true
          for each goal in graph.goalLiterals do
           if goal not in layeri then allGoalsMet <- false
          if not allGoalsMet then continue

          goalsAreMutex <- false
          for each goalA in graph.goalLiterals do
           for each goalB in graph.goalLiterals do
            if layeri.isMutex(goalA, goalB) then goalsAreMutex <- true
          if not goalsAreMutex then return i
    """
    layers = self.fill().literal_layers
    for cost, literal_layer in enumerate(layers):
        if self.goal.issubset(literal_layer):
            '''
            goals_are_mutex = False
            # this code is only for debug purposes
            for goal1 in self.goal: 
                for goal2 in self.goal:
                    if goal1 != goal2
                        print("testing", goal1, goal2, literal_layer.is_mutex(goal1, goal2))
                        if literal_layer.is_mutex(goal1, goal2):
                            goals_are_mutex = True 
            if goals_are_mutex:
                continue
            else:
                return cost   
            '''
            if any([literal_layer.is_mutex(goal1, goal2) for goal1 in self.goal for goal2 in self.goal if goal1 != goal2]):
                print(cost, "have a mutex")
                continue
            else:
                print(cost, "do not have a mutex!")
                return cost
```
