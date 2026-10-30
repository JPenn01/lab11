# Error table

One row per failure. Fill in every column. You need at least eight rows.

| Scenario | Function that detects it | Error value | What the player sees |
|---|---|---|---|
| Fleet file does not exist | `load_fleet` | `Err(DataError::Io(..))` (kind `NotFound`) | _(example: your row goes here)_ |
| The fleet path is a folder | load_fleet | Err(DataError::Io(..)) | On stderr: Error: could not load data/fleet.txt: No such file or directory (os error 2). The game exits with code 1. |
| Fleet file has only comments | load_fleet | Err(DataError::NoShips("data/fleet_empty.txt")) | On stderr: Error: could not load data/fleet_empty.txt: no valid ships in data/fleet_empty.txt. Exit code 1. |
| Every line in the fleet file is bad | load_fleet | Err(DataError::NoShips("data/fleet_all_bad.txt")) | On stderr: Error: could not load data/fleet_all_bad.txt: no valid ships in data/fleet_all_bad.txt. Exit code 1. |
| Board file has nine rows | parse_board (called by load_board) | Err(DataError::Board(BoardError::WrongRowCount(9))) | Practice board unavailable: bad board layout: found 9 rows, but a board needs exactly 10, then back to the menu. |
| Board file has a bad character (x on file line 6) | parse_board (called by load_board) | Err(DataError::Board(BoardError::BadChar { line: 6, ch: 'x' })) | Practice board unavailable: bad board layout: line 6 has the character 'x', but only '.' and 'S' are allowed, then back to the menu. |
| Scores file does not exist | load_scores | Ok(Vec::new()) (not an error, because NotFound is normal) | no scores yet under TOP 5. The menu draws as usual. |
| Scores file cannot be written | append_score | Err(DataError::Io(..)) | Could not save the score: Is a directory (os error 21), then on to the menu. |

Scenarios to cover (add more if you find them):

- fleet file missing
- a directory given as the fleet path
- fleet file with only comments
- fleet file where every line is bad
- board file with nine rows
- board file with a bad character
- scores file missing
- scores file that cannot be written
- `K11` typed at the prompt
