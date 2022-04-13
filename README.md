# alcachofaQuestions

1.- Tell me about a time you had to explain something technical to a nontechnical
person.

I have worked with the client directly and when I had to recollect information or explain what is my proposal or solution; I tried to use an easy words, and translate this explanation easy to understand to anybody.




2.- Which Sorting algorithm do you like the most? What is its complexity?

I prefer Merge sort because is an efficient algorithm to sort; it operates very well on any data type. Does not matter the size because it apply “divide and conquer” technique. The time of complexity of this algorithm is O(n log n).



3.- Where are usually allocated log files in a unix system?

they are in /var/log




4.- What is your opinion about Golang for the web?

Golang is a pragmatic language, easy to use and learn. You can create n API in 10 minutes or less, you can design quicky and scalable web applicationsThis language has a good perfomance because it works with concurrency model, you can create goroutines and theys are more cheape and faster than Python threads.

Golang has support for technologies from HTTP/2, database like MySQL, MongoDB and it gives you facility to deploy faster.





5.- Write the UNIX command that adds the read access permission to the group
members of a directory and to all its content.


~~~bash
# 1.- Change group owner of the directory
chgrp -R grpTest testFolder/* 
# 2. Give write permission to the group
chmod -R g+r testFolder/*
  ~~~

6.- Implement a function called uniqueFruits, that passing two slices of fruits, it
will return a slice containing the fruits that appear in either or both slices. The
returned slice should have no duplicates.
For example, calling uniqueFruits([]string{"Banana", "Apple", "Pear"},
[]string{"Banana", "Cherry", "Pear", “Pear”}) should return a slice containing
Banana, Apple, Pear, and Cherry in any order.

~~~go
func TestUniqueFruits(t *testing.T) {
	want := []string{"Apple", "Banana", "Cherry", "Pear"}
	got := UniqueFruits([]string{"Banana", "Apple", "Pear"},
		[]string{"Banana", "Cherry", "Pear", "Pear"})

	assert.Equal(t, want, got)
}

func UniqueFruits(fruits ...[]string) []string {
	var mapFruits = make(map[string]int)

	for _, frs := range fruits {
		for _, v := range frs {
			mapFruits[v] = 1
		}
	}

	var uniqueFruits = []string{}
	for k, _ := range mapFruits {
		uniqueFruits = append(uniqueFruits, k)
	}

	sort.Strings(uniqueFruits)

	return uniqueFruits
}
~~~




7.- Write an HTML page with a div containing the text Alcachofa in green colour.
The div must be horizontally and vertically centred.

~~~hmtl5
<!doctype html>
<html>
   <body>
      <div class="centered">
      <p style="text-align: center;"><span          style="color:     #00ff00;">Alcachofa</span></p>
    </div>
   </body>
</html>
~~~




8.- From the following tables write a SQL query:
to find the city with the maximum number of plant species that don't grow in the same city 
where their farmers live and have more than 25 species. 
(In a city a farmer can grow different types of plants).

Plant - Id, name, city, number_of_species, farmer_id
Farmer - Id, name, city

~~~sql
select maxByCity.city, maxByCity.number_species
from (
	select
		f.city,
		max(p.number_of_species) number_species
	from plant p, farmer f
	where p.farmer_id = f.id
	and p.city != f.city 
	having count(p.number_of_species) > 25
	group by f.city
	) maxByCity
order by maxByCity.number_species desc
limit by 1;	
~~~
