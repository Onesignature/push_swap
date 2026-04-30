# push_swap

A 42 sorting-algorithm project. Given a stack of integers, output the **shortest possible sequence** of allowed stack operations that sorts them.

## The challenge

You have two stacks, `A` and `B`. `A` starts with the input integers; `B` starts empty. Sort `A` in ascending order using only the operations below — and minimize the move count.

## Allowed operations

| Op | Effect |
|---|---|
| `sa` | Swap the top two elements of `A` |
| `sb` | Swap the top two elements of `B` |
| `ss` | `sa` and `sb` simultaneously |
| `pa` | Push the top of `B` onto `A` |
| `pb` | Push the top of `A` onto `B` |
| `ra` | Rotate `A` upward (top element becomes last) |
| `rb` | Rotate `B` upward |
| `rr` | `ra` and `rb` simultaneously |
| `rra` | Reverse rotate `A` (last element becomes first) |
| `rrb` | Reverse rotate `B` |
| `rrr` | `rra` and `rrb` simultaneously |

## Approach

Stacks are stored as arrays. The strategy depends on input size:

- **≤ 5 elements** — brute-force the optimal sequence
- **Larger inputs** — a chunk-based / quicksort-style strategy: push partitions of `A` to `B`, sort there, then merge back

Edge cases handled: empty input, single element, already-sorted input, duplicate-value rejection, and non-integer / overflow input rejection.

## Build

```bash
make
```

## Run

```bash
./push_swap 3 2 5 1 4
```

Output is the operation sequence:

```
pb
pb
ra
pa
pa
```

Pipe into the 42 `checker` to verify:

```bash
./push_swap 3 2 5 1 4 | ./checker 3 2 5 1 4
```

Or with a variable:

```bash
ARG="3 2 5 1 4"; ./push_swap $ARG | ./checker $ARG
```

## Layout

- `push_swap.c`, `push_swap.h` — entry point and headers
- `parsing/` — argument parsing, validation, error handling
- `operations/` — implementations of `sa`/`sb`/`ra`/`rb`/`pa`/`pb`/`rra`/`rrb`/...
- `sorting/` — small-case brute force + chunk-based sort
- `libft/` — utility functions

## Resources

- [42 push_swap subject](https://cdn.intra.42.fr/pdf/pdf/133152/en.subject.pdf)
