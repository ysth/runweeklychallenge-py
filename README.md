Facilitates running a solution to [the Weekly Challenge](https://theweeklychallenge.org) using one or more sets of inputs provided as JSON command line arguments.

Example usage running a "solution" to sum integers:

    import run_weeklychallenge as run
    import run
    
    def sum_of_ints(ints: list[int]) -> int:
        sum: int = 0
        i: int
        for i in ints:
            sum += i
        return sum
    
    def main() -> None:
        def run_solution(inputs: object) -> str:
            return str(sum_of_ints(cast(list[int], cast(dict, inputs).get("ints"))))
        run.run_weekly_challenge(
            run_solution,
            inputs_example = '{"ints":[1,2,3]}',
            inputs_schema_json = '''{
                "type": "object",
                "properties": {
                    "ints": {
                        "type": "array",
                        "items": { "type": "integer" }
                    }
                },
                "required": ["ints"],
                "additionalProperties": false
            }'''
        )
    
    if __name__ == '__main__':
        main()

Example output:

    $ python example.py '{"ints":[1,2,3]}' '{"ints":[]}'
    Inputs: {"ints":[1,2,3]}
    Output: 6
    Inputs: {"ints":[]}
    Output: 0

You must provide an example JSON inputs string (used in error messages), a JSON schema for inputs, and a shim function to run the solution given the decoded JSON inputs and reformat the output if desired.
