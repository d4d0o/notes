#### Find files grep something and output in a different file based on source's filename 

$find . -type f -exec sh -c 'grep "something" <"$0" >"$0.txt"' {} \;

