setup [max] (needs large context, follow instructions carefully)
    inputs
        + benchmark description and constraints
        + code/repo to use
        + metric(s) to optimize
        + log db/plot specifics
    tasks
        - setup new repo in a subfolder in /root/capsule/results, or clone from github and install env
        - make the benchmark script - should print relevant metric(s) to stdout OR write a file containing them. ensure that collecting and writing metrics does not interfere with the results of the benchmark. ensure script is runnable, 
        - setup result logging and plotting
    handoffs
        - eval script path 
        - terse list of details/gotchas subsequent agents must be aware of about
            - benchmark
            - code/repo/environment
            - metric(s)
            - logging/plotting

generate ideas queue [max] (needs to be creative and detailed)
    inputs
        + metric(s) to optimize
        + constraints
    tasks
        - generate ideas for improving the metric(s), given the constraints
        - order by expected impact
        - make sublists of sub-ideas/variations to try within each idea

run eval script [low] (just needs to run and maybe debug basic issues)

commit [low] (commits source changes, raw result artifacts, or final judgment artifacts separately)

loop:
    propose [medium]
        inputs:
            + ideas
            + constraints
        outputs:
            - proposal
    implement [medium]
        inputs:
            + proposal name
        + constraints
    eval [low]
        - run (fix basic invocation issues)
        - appends raw result with eval status
        - regenerates plots with pending/crashed status
    commit [low]
        - code separately
        - raw log/plot results separately
    judge [low]
        - append final outcome: kept, discarded, or crashed
        - regenerate plots with final outcome
        - keep or revert code change
    commit [low]
        - judgment/status log and regenerated plots separately
