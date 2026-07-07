NOTES.md

* Explain one fix.

dates_overlap() only checked if the new booking's start date fell inside
the existing booking. It missed the case where the new booking starts
earlier but still runs into the tail end of the existing one, so those
got through when they shouldn't have. Fixed it with the normal overlap
check: start_a <= end_b and start_b <= end_a.

* Show the failure.

Canon DSLR was already booked Jan 10-15. Before the fix, booking it again
for Jan 5-12 was allowed even though that overlaps Jan 10-12. Now blocked/hidden.


* AI use

Used it to help debug and double check my fixes. Mainly for the overlap
logic since off-by-one bugs there are easy to miss. Still tested
everything myself by hand through the running app before committing -
booking overlapping ranges in different ways (inside, straddling start,
straddling end, non-overlapping) to make sure the fix actually worked.