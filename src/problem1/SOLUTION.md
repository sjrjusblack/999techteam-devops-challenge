Provide your CLI command here:
jq -r 'select(.symbol == "TSLA" and .side == "sell") | .order_id' ./transaction-log.txt | xargs -I {} curl "https://example.com/api/{}" >> ./output.txt
