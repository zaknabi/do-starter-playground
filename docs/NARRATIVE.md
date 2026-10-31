# Step-free London: core narrative

Working draft, following the Data Observatory Content Planner. Anything marked **TBC** is a
hypothesis that the analysis will confirm or change.

## Core narrative

- **Key message:** If you can't use stairs, London becomes a smaller and slower city. From
  Imperial's own station, South Kensington, a journey to Bank takes 21 minutes by Tube, or 51
  minutes on three buses if you need step-free access.
- **Audience:** People who visit the Data Observatory: Imperial staff and students, visiting
  partners and policymakers. Most of them use the Tube without thinking about stairs. They care
  about London working well and working fairly, and some of them make decisions that shape it.
- **Takeaway:**
    - _Learn:_ step-free access is not a yes/no label on a station map. It changes how far you
      can get in a given time, and the gap is uneven across London (**TBC**).
    - _Feel:_ surprise that the same city shrinks so much for some people, and a sense that the
      gap can be measured, so it can be closed.
- **Evidence & visuals needed:**
    - Two travel-time maps side by side from one origin: _everyone_ vs _step-free_.
    - A reach comparison: how many stations each group can reach within 45 minutes (**TBC**).
    - A penalty map: extra minutes for each destination when travelling step-free.
    - Step-free status of every station.
    - Optional live layer: lifts out of service right now.

## Story arc (left to right across the wall)

| Section             | Content                                                                                                                                                                            |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Title**           | _Step-free London: who can get where?_ Credits: Zak Nabi, Imperial College London. Built on the DSI Developer Playground. Powered by the Transport for London Journey Planner API. |
| **Problem/context** | Hook: South Kensington to Bank, 21 vs 51 minutes. Who needs step-free journeys: wheelchair users, people with pushchairs, heavy luggage or an injury, and many older people.       |
| **Exploration**     | The two maps, live. From a tablet, the operator picks an origin station and both maps redraw.                                                                                      |
| **Insight**         | **TBC.** For example: "From _X_, step-free travellers reach _Y_% of what everyone else reaches in 45 minutes", and where in London the gap is largest.                             |
| **Implications**    | What the gap costs people: longer journeys and fewer places within reach. Lift outages widen it further day to day (live feed).                                                    |
| **Future**          | **Stretch goal:** which single station upgrade would close the most gap? This would be computed by re-running the analysis with each candidate station made step-free.             |

## Data sources

| Data                    | Source                                                                                                   | Use                                   |
| ----------------------- | -------------------------------------------------------------------------------------------------------- | ------------------------------------- |
| Journey times           | TfL Unified API `/Journey/JourneyResults`, with and without `accessibilityPreference=StepFreeToPlatform` | Travel-time maps, reach, penalty      |
| Station topology        | `api.tfl.gov.uk/stationdata/tfl-stationdata-detailed.zip` (509 stations, 573 lifts)                      | Station step-free status, coordinates |
| Lift outages (optional) | TfL Unified API `/Disruptions/Lifts/v2`                                                                  | Live implications layer               |

## Method decisions (to confirm)

- **When:** a fixed weekday morning departure (e.g. Tuesday 09:00), so results are reproducible and
  not skewed by evening or weekend service.
- **Where to:** every station in the topology data. Origins are a curated shortlist (South
  Kensington plus 4–6 stations across London) so the API workload stays manageable.
- **Reach threshold:** 45 minutes, a typical commute.
- **Caveat to state on the wall:** these are TfL's _planned_ step-free routes. Real journeys can be
  worse when lifts are out of service.
