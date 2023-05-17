SELECT
    hour,
    claimed,
    SUM(claimed) over(ORDER BY hour ASC) AS claimed_cumulative
FROM (
    SELECT
        date_trunc('hour', evt_block_time) AS hour,
        (SUM(value / 1e18)) AS claimed
    FROM collab_land_optimism.OrigamiGovernanceToken_evt_Transfer
    WHERE from 
    GROUP BY hour
)
ORDER BY hour
