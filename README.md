# Python-Devops
Try to cover pretty much we know, everything Dockerize!

## Covered
1. AutoPEP8
2. Graph-dependencies
3. Pytest Flask
4. Locust stress test
5. Flask basic
6. Flask and MongoDB
7. Flask Rest API
8. Flask + Rest API + Redis + PubSub
9. Flask + MySQL + Rest API
10. Flask + Postgres + Rest API
11. Flask + Elastic Search
12. Streaming Twitter + Elastic Search + Kibana
13. News Crawler + Luigi + Elastic Search + Kibana
14. Flask SocketIO Scaling + Redis
15. Distributed Flask + Redis + Nginx load balancer
16. Distributed Flask SocketIO + Redis + Nginx load balancer
17. Flask + Gunicorn + ELK
18. Flask + Hadoop
19. Mlflow + Nginx
20. Flask + Kafka
21. Flask + Hive + Hadoop

## Misc

1. Elasticsearch + Kibana
2. Elasticsearch + Cerebro
3. Jupyter notebook
4. Jupyterhub

## How-to Docker
Every folders contain .yml for docker-compose. You need to install Docker-Compose first.

To run,
```bash
compose/build
```

To safely close
```bash
compose/down
```

To remove all images
```bash
docker rmi $(docker images -q)
```

To remove `none` images
```bash
docker rmi $(docker images -f "dangling=true" -q)
```

To remove all containers
```bash
docker rm $(docker ps -aq)
```

## How-to-Use

<details><summary>1. AutoPEP8</summary>

```bash
cd autopep8
autopep8 --in-place --aggressive --recursive .
```

</details>

<details><summary>2. Graph-dependencies</summary>

```bash
cd graph-dependencies
python3 pyan.py malaya/*.py --colored --annotate --grouped --dot > malaya.dot
dot -Tsvg malaya.dot > malaya.svg
```

![alt text](2.graph-dependencies/malaya.svg)

![alt text](2.graph-dependencies/malaya-graph.png)

</details>

<details><summary>3. Pytest Flask</summary>

```text
pytest_1  | Name                 Stmts   Miss  Cover
pytest_1  | ----------------------------------------
pytest_1  | web/__init__.py         13      2    85%
pytest_1  | web/calculation.py       6      1    83%
pytest_1  | ----------------------------------------
pytest_1  | TOTAL                   19      3    84%
pytest_1  | Coverage HTML written to dir htmlcov
```

Open report/index.html

![alt text](3.pytest-flask/coverage.png)

</details>

<details><summary>4. Locust stress-test</summary>

![alt text](4.Locust-Stresstest/screenshot1.png)

![alt text](4.Locust-Stresstest/screenshot2.png)

</details>

<details><summary>5. Flask</summary>

```text
curl localhost:5000/ -x GET

Hey, we have Flask in a Docker container!
```
```text
curl localhost:5000/members/husein/

husein
```

</details>

<details><summary>6. Flask with MongoDB</summary>

```text
curl localhost:5000/ -X GET

Hey, we have Flask with MongoDB in a Docker container!
```
```text
curl localhost:5000/insert?name=husein -X GET

done inserted husein
```
```text
curl localhost:5000/get?name=husein -X GET

husein
```
```text
curl localhost:5000/get?name=mike -X GET

not found
```

</details>

<details><summary>7. Flask Rest API</summary>

```text
curl localhost:5000 -X GET

{"hello": "world"}
```
```text
curl localhost:5000/todo1 -d "data=take milk" -X PUT
curl localhost:5000/todo1 -X GET

{"todo1": "take milk"}
```

</details>

<details><summary>8. Flask + Rest API + Redis + Pubsub</summary>

```text
curl localhost:5000 -X GET

Hey, we have Flask with Redis in a Docker container!
```

```text
localhost:5000/first-channel -X GET

{"message": "Internal Server Error"}
```

```text
curl localhost:5000/first-channel -d "data=from first channel" -X PUT

"from first channel"

curl localhost:5000/first-channel -X GET

"from first channel"
```

```text
curl localhost:5000/fifth-channel -X GET

{"message": "Internal Server Error"}
```

</details>

<details><summary>9. Flask + MySQL + Rest API</summary>

```text
curl localhost:5000/ -d "username=huseinzol05&first_name=husein&last_name=zolkepli&password=comel" -X PUT

"success {\"password\": \"comel\", \"first_name\": \"husein\", \"last_name\": \"zolkepli\", \"username\": \"huseinzol05\"}"

curl localhost:5000/ -d "username=huseinzol05" -X GET

"[10001, \"huseinzol05\", \"husein\", \"zolkepli\", \"comel\"]"
```

</details>

<details><summary>10. Flask + Postgres + Rest API</summary>

```text
curl localhost:5000/ -d "username=huseinzol05&first_name=husein&last_name=zolkepli&pass=comel" -X PUT

"success {\"pass\": \"comel\", \"first_name\": \"husein\", \"last_name\": \"zolkepli\", \"username\": \"huseinzol05\"}"

curl localhost:5000/ -d "username=huseinzol05" -X GET

"[\"huseinzol05\", \"husein\", \"zolkepli\", \"comel\"]"
```

</details>

<details><summary>11. Flask + Elastic Search</summary>

```text
curl localhost:9200/recipes/_search?q=title:salad -X GET

{"took":62,"timed_out":false,"_shards":{"total":1,"successful":1,"skipped":0,"failed":0},"hits":{"total":10,"max_score":0.054237623,"hits":[{"_index":"recipes","_type":"salads","_id":"LtlzD2UBBv9LAuM_3gMX","_score":0.054237623,"_source":{"ingredients": [{"step": "1/4 cup basil leaves"}, {"step": "4 cups 1/2-inch cubes watermelon"}, {"step": "2 teaspoons lemon juice"}, {"step": "1/4 teaspoon kosher salt"}, {"step": "1/4 teaspoon chili powder"}], "description": "A quick salad of watermelon and basil. The chili powder plays well with the sweetness of the melon.", "submitter": "Chefthompson.com", "title": "Watermelon Basil Salad", "calories": "10"}}
```

</details>

<details><summary>12. Streaming Twitter + Elastic Search + Kibana</summary>

Make sure you inserted related keys in twitter-streaming.py

```python
consumer_key=""
consumer_secret=""

access_token=""
access_token_secret=""
```

![alt text](12.sentiment-twitter-elasticsearch/kibana.png)

</details>

<details><summary>13. News Crawler + Luigi + Elastic Search + Kibana</summary>

Task automation

![alt text](13.luigi-crawler-sentiment-elasticsearch/dependency.png)

localhost:8082

![alt text](13.luigi-crawler-sentiment-elasticsearch/luigi.png)

Kibana

![alt text](13.luigi-crawler-sentiment-elasticsearch/kibana.png)

</details>

<details><summary>14. Flask SocketIO Scaling + Redis</summary>

```python
# gunicorn with eventlet, 400 unique threads, 100 threads per second
stress_test(400,100)

# index 0, total time taken 99.869447 s, average time taken 0.998694 s
# index 100, total time taken 222.226329 s, average time taken 2.222263 s
# index 200, total time taken 271.741829 s, average time taken 2.717418 s
# index 300, total time taken 376.807925 s, average time taken 3.768079 s
```

</details>

<details><summary>15. Distributed Flask + Redis + Nginx load balancer</summary>

```text
Port 80 will load balanced on 2 different servers, 5000 and 5001.

curl http://localhost:5000/ -X GET
Hello World! I have been seen 19 times.

curl http://localhost:5001/ -X GET
Hello World! I have been seen 20 times.

curl http://localhost/ -X GET
Hello World! I have been seen 21 times.
```

</details>

<details><summary>16. Distributed Flask SocketIO + Redis + Nginx load balancer</summary>

```text
Port 80 will load balanced on 2 different servers, 5000 and 5001.

stress_test(get_time_80, 50,10)
index 0, total time taken 1.087309 s, average time taken 0.108731 s
index 10, total time taken 1.203958 s, average time taken 0.120396 s
index 20, total time taken 1.310126 s, average time taken 0.131013 s
index 30, total time taken 1.595863 s, average time taken 0.159586 s
index 40, total time taken 1.548332 s, average time taken 0.154833 s
```

</details>

<details><summary>17. Flask + Gunicorn + ELK</summary>

```html
http://localhost:9200/_cat/indices?v
```

```text
health status index               uuid                   pri rep docs.count docs.deleted store.size pri.store.size
yellow open   logstash-2018.09.30 IL6UjeHTTCKdL8be5hpOUw   5   1          0            0       460b           460b
```

```html
http://localhost:9200/logstash-2018.09.30/_search
```

```text
{"took":147,"timed_out":false,"_shards":{"total":5,"successful":5,"skipped":0,"failed":0},"hits":{"total":4,"max_score":1.0,"hits":[{"_index":"logstash-2018.09.30","_type":"doc","_id":"lUw4KGYBBCQZE1CyH2wT","_score":1.0,"_source":{"@timestamp":"2018-09-30T02:04:18.472Z","host":"localhost","@version":"1","port":36286,"message":"172.22.0.1 - - [30/Sep/2018:02:04:18 +0000] \"GET / HTTP/1.1\" 200 41 \"-\" \"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36\""}},{"_index":"logstash-2018.09.30","_type":"doc","_id":"k0w4KGYBBCQZE1CyHWyY","_score":1.0,"_source":{"@timestamp":"2018-09-30T02:04:17.203Z","host":"localhost","@version":"1","port":36286,"message":"172.22.0.1 - - [30/Sep/2018:02:04:16 +0000] \"GET / HTTP/1.1\" 200 41 \"-\" \"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36\""}},{"_index":"logstash-2018.09.30","_type":"doc","_id":"lkw4KGYBBCQZE1CyH2zP","_score":1.0,"_source":{"@timestamp":"2018-09-30T02:04:18.658Z","host":"localhost","@version":"1","port":36286,"message":"172.22.0.1 - - [30/Sep/2018:02:04:18 +0000] \"GET / HTTP/1.1\" 200 41 \"-\" \"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36\""}},{"_index":"logstash-2018.09.30","_type":"doc","_id":"lEw4KGYBBCQZE1CyHWzg","_score":1.0,"_source":{"@timestamp":"2018-09-30T02:04:18.160Z","host":"localhost","@version":"1","port":36286,"message":"172.22.0.1 - - [30/Sep/2018:02:04:18 +0000] \"GET / HTTP/1.1\" 200 41 \"-\" \"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36\""}}]}}
```

</details>

<details><summary>18. Flask + Hadoop</summary>

```bash
curl --form file=@18.flask-hadoop/text.txt localhost:5000/lowercase
```

```text
["husein\nbin\nzolkepli\n"]
```

![alt text](18.flask-hadoop/screenshot1.png)

![alt text](18.flask-hadoop/screenshot2.png)

</details>

<details><summary>19. Mlflow + Nginx</summary>

![alt text](19.mlflow-nginx/mlflow.png)

</details>

<details><summary>20. Flask + Kafka</summary>

```bash
curl http://localhost:5000/topic/recipes/
```

```text
[{"calories": "137", "ingredients": [{"step": "3 cups chopped cabbage"}, {"step": "1 unpeeled red apple, cored and chopped"}, {"step": "1 unpeeled Granny Smith apple, cored and chopped"}, {"step": "1 carrot, grated"}, {"step": "1/2 cup finely chopped red bell pepper"}, {"step": "2 green onions, finely chopped"}, {"step": "1/3 cup mayonnaise"}, {"step": "1/3 cup brown sugar"}, {"step": "1 tablespoon lemon juice, or to taste"}], "submitter": "Aunt Mamie", "description": "This is our favorite cole slaw recipe, a yummy combo of fruit and veggies in a sweet dressing.", "title": "Easy Apple Coleslaw"}, {"calories": "434", "ingredients": [{"step": "6 cups cubed russet potatoes"}, {"step": "1 teaspoon salt"}, {"step": "1 cup sour cream"}, {"step": "1 cup creamy salad dressing (such as Miracle Whip\u00ae)"}, {"step": "1/2 teaspoon coarse ground black pepper"}, {"step": "1 cup shredded Cheddar cheese"}, {"step": "1/2 cup chopped green onions"}, {"step": "1/2 cup real bacon bits"}], "submitter": "spicejenmom", "description": "This is a great twist on two all-American favorites--the potato salad and the loaded baked potato. Served cold, this has been a crowd-pleaser at our many family functions and is often requested. Even people who don't normally love potato salad seem to love this!", "title": "All-American Loaded Baked Potato Salad"}, {"calories": "208", "ingredients": [{"step": "Salad:"}, {"step": "4 English cucumbers, diced"}, {"step": "4 Roma (plum) tomatoes, seeded and diced"}, {"step": "1/2 purple onion, diced"}, {"step": "1 red bell pepper, seeded and diced"}, {"step": "2 tablespoons chopped garlic"}, {"step": "1 cup chopped fresh parsley"}, {"step": "3 tablespoons chopped fresh mint"}, {"step": "Dressing:"}, {"step": "1/2 cup olive oil"}, {"step": "2 tablespoons fresh lemon juice"}, {"step": "1 tablespoon kosher salt"}, {"step": "1 tablespoon ground black pepper"}], "submitter": "mimitomany", "description": "Chopped tomatoes, cucumbers, onions, and parsley combine with a drizzled dressing of lemon juice, olive oil, garlic, and mint leaves.", "title": "Israeli Tomato and Cucumber Salad"}, {"calories": "10", "ingredients": [{"step": "1/4 cup basil leaves"}, {"step": "4 cups 1/2-inch cubes watermelon"}, {"step": "2 teaspoons lemon juice"}, {"step": "1/4 teaspoon kosher salt"}, {"step": "1/4 teaspoon chili powder"}], "submitter": "Chefthompson.com", "description": "A quick salad of watermelon and basil. The chili powder plays well with the sweetness of the melon.", "title": "Watermelon Basil Salad"}, {"calories": "303", "ingredients": [{"step": "1 (10 ounce) can artichoke hearts, drained and chopped"}, {"step": "1 cup cherry tomatoes, halved"}, {"step": "1/2 cup pitted Kalamata olives, halved"}, {"step": "3 zucchini, spiralized"}, {"step": "2 lemons, juiced"}, {"step": "1/4 cup extra-virgin olive oil"}, {"step": "2 tablespoons chopped parsley"}, {"step": "1 tablespoon white vinegar"}, {"step": "2 cloves garlic, minced"}, {"step": "2 teaspoons dried oregano"}, {"step": "1 teaspoon kosher salt"}, {"step": "1 lemon, zested"}, {"step": "1/2 teaspoon ground black pepper"}, {"step": "1/4 cup crumbled goat milk feta cheese, or to taste"}], "submitter": "Cindy Anschutz Barbieri", "description": "The perfect 'pasta' salad for summer!", "title": "Mediterranean Zucchini 'Pasta' Salad"}, {"calories": "128", "ingredients": [{"step": "1 (10 ounce) package mixed salad greens"}, {"step": "1 pint fresh blueberries"}, {"step": "1/4 cup walnuts"}, {"step": "1/2 cup raspberry vinaigrette salad dressing"}, {"step": "1/4 cup crumbled feta cheese"}], "submitter": "MARASADIE", "description": "An easy, yummy salad, perfect for any season, with berries, nuts, and greens. For an entree add chicken, diced apples, and diced green onions!", "title": "Blueberry Walnut Salad"}, {"calories": "159", "ingredients": [{"step": "1 (15 ounce) can lentils, drained and rinsed"}, {"step": "1 red onion, diced"}, {"step": "2 tomatoes, diced"}, {"step": "2 small cucumbers, diced"}, {"step": "1/4 cup olive oil"}, {"step": "2 tablespoons apple cider vinegar"}, {"step": "2 tablespoons fresh lime juice"}, {"step": "salt and ground black pepper to taste"}], "submitter": "NOOSH", "description": "A refreshing salad made with diced vegetables and lentils, perfect for a side dish or on its own. To add more freshness, add chopped mint to the salad.", "title": "Lentil Salad with a Persian Twist"}, {"calories": "310", "ingredients": [{"step": "1 (16 ounce) package fusilli (spiral) pasta"}, {"step": "3 cups cherry tomatoes, halved"}, {"step": "1/2 pound provolone cheese, cubed"}, {"step": "1/2 pound salami, cubed"}, {"step": "1/4 pound sliced pepperoni, cut in half"}, {"step": "1 large green bell pepper, cut into 1 inch pieces"}, {"step": "1 (10 ounce) can black olives, drained"}, {"step": "1 (4 ounce) jar pimentos, drained"}, {"step": "1 (8 ounce) bottle Italian salad dressing"}], "submitter": "Irlandes", "description": "This is the best pasta salad I've ever eaten, and people request it frequently. It's a very easy, light-tasting side dish for a picnic or dinner.", "title": "Awesome Pasta Salad"}, {"calories": "131", "ingredients": [{"step": "3 cucumbers, seeded and sliced"}, {"step": "1 1/2 cups crumbled feta cheese"}, {"step": "1 cup black olives, pitted and sliced"}, {"step": "3 cups diced roma tomatoes"}, {"step": "1/3 cup diced oil packed sun-dried tomatoes, drained, oil reserved"}, {"step": "1/2 red onion, sliced"}], "submitter": "Heather", "description": "This is a great salad to take to a barbeque. All ingredients are approximate, so add more or less of any ingredient depending on your own taste.", "title": "Mediterranean Greek Salad"}, {"calories": "338", "ingredients": [{"step": "1 tablespoon butter"}, {"step": "3/4 cup almonds, blanched and slivered"}, {"step": "1 pound spinach, rinsed and torn into bite-size pieces"}, {"step": "1 cup dried cranberries"}, {"step": "2 tablespoons toasted sesame seeds"}, {"step": "1 tablespoon poppy seeds"}, {"step": "1/2 cup white sugar"}, {"step": "2 teaspoons minced onion"}, {"step": "1/4 teaspoon paprika"}, {"step": "1/4 cup white wine vinegar"}, {"step": "1/4 cup cider vinegar"}, {"step": "1/2 cup vegetable oil"}], "submitter": "Jamie Hensley", "description": "Everyone I have made this for RAVES about it! It's different and so easy to make!", "title": "Jamie's Cranberry Spinach Salad"}, {"calories": "200", "ingredients": [{"step": "1 (16 ounce) bag coleslaw mix"}, {"step": "2 tablespoons diced onion"}, {"step": "2/3 cup creamy salad dressing (such as Miracle Whip\u2122)"}, {"step": "3 tablespoons vegetable oil"}, {"step": "1/2 cup white sugar"}, {"step": "1 tablespoon white vinegar"}, {"step": "1/4 teaspoon salt"}, {"step": "1/2 teaspoon poppy seeds"}], "submitter": "Sandi Gregory Johnson", "description": "This tastes just like the cole slaw served at popular fried chicken or fish restaurants. It's excellent with burgers or on top of BBQ'd pork sandwiches, too!!!", "title": "Sweet Restaurant Slaw"}, {"calories": "491", "ingredients": [{"step": "2 tablespoons sesame seeds"}, {"step": "1 tablespoon poppy seeds"}, {"step": "1/2 cup white sugar"}, {"step": "1/2 cup olive oil"}, {"step": "1/4 cup distilled white vinegar"}, {"step": "1/4 teaspoon paprika"}, {"step": "1/4 teaspoon Worcestershire sauce"}, {"step": "1 tablespoon minced onion"}, {"step": "10 ounces fresh spinach - rinsed, dried and torn into bite-size pieces"}, {"step": "1 quart strawberries - cleaned, hulled and sliced"}, {"step": "1/4 cup almonds, blanched and slivered"}], "submitter": "TOZENUF", "description": "Someone brought this salad to a pot luck dinner and I had to have the recipe. I have made it many, many times since then and I have been asked for the recipe every time I bring it somewhere. It is also a great way to get kids to eat spinach!", "title": "Strawberry Spinach Salad I"}, {"calories": "390", "ingredients": [{"step": "4 cups uncooked elbow macaroni"}, {"step": "1 cup mayonnaise"}, {"step": "1/4 cup distilled white vinegar"}, {"step": "2/3 cup white sugar"}, {"step": "2 1/2 tablespoons prepared yellow mustard"}, {"step": "1 1/2 teaspoons salt"}, {"step": "1/2 teaspoon ground black pepper"}, {"step": "1 large onion, chopped"}, {"step": "2 stalks celery, chopped"}, {"step": "1 green bell pepper, seeded and chopped"}, {"step": "1/4 cup grated carrot (optional)"}, {"step": "2 tablespoons chopped pimento peppers (optional)"}], "submitter": "Graden", "description": "This is a salad that everyone seems to love. I always get lots of compliments on this recipe and it is just a pleasing taste that seems to suit everyone.", "title": "Classic Macaroni Salad"}, {"calories": "334", "ingredients": [{"step": "1 (15 ounce) can black beans, rinsed and drained"}, {"step": "1 (15 ounce) can kidney beans, drained"}, {"step": "1 (15 ounce) can cannellini beans, drained and rinsed"}, {"step": "1 green bell pepper, chopped"}, {"step": "1 red bell pepper, chopped"}, {"step": "1 (10 ounce) package frozen corn kernels"}, {"step": "1 red onion, chopped"}, {"step": "1/2 cup olive oil"}, {"step": "1/2 cup red wine vinegar"}, {"step": "2 tablespoons fresh lime juice"}, {"step": "1 tablespoon lemon juice"}, {"step": "2 tablespoons white sugar"}, {"step": "1 tablespoon salt"}, {"step": "1 clove crushed garlic"}, {"step": "1/4 cup chopped fresh cilantro"}, {"step": "1/2 tablespoon ground cumin"}, {"step": "1/2 tablespoon ground black pepper"}, {"step": "1 dash hot pepper sauce"}, {"step": "1/2 teaspoon chili powder"}], "submitter": "Karen Castle", "description": "A colorful, spicy, and refreshing bean and corn salad.", "title": "Mexican Bean Salad"}, {"calories": "430", "ingredients": [{"step": "2 pounds clean, scrubbed new red potatoes"}, {"step": "6 eggs"}, {"step": "1 pound bacon"}, {"step": "1 onion, finely chopped"}, {"step": "1 stalk celery, finely chopped"}, {"step": "2 cups mayonnaise"}, {"step": "salt and pepper to taste"}], "submitter": "Donna", "description": "This creamy salad is made with red potatoes, which give this dish--chock full of melt-in-your-mouth bacon, bits of hard boiled egg, crunchy celery and spicy onion--a delectable, firm texture.", "title": "Red Skinned Potato Salad"}, {"calories": "559", "ingredients": [{"step": "10 slices bacon"}, {"step": "1 head fresh broccoli, cut into bite size pieces"}, {"step": "1/4 cup red onion, chopped"}, {"step": "1/2 cup raisins"}, {"step": "3 tablespoons white wine vinegar"}, {"step": "2 tablespoons white sugar"}, {"step": "1 cup mayonnaise"}, {"step": "1 cup sunflower seeds"}], "submitter": "JJOHN32", "description": "Confirmed broccoli haters have changed their minds after tasting this salad. It is great for potlucks or buffet meals. Make a day or so before you wish to serve to meld the ingredients. I have used sugar substitutes for the white sugar and also used nonfat or low-fat mayonnaise and it still tastes great!", "title": "Alyson's Broccoli Salad"}, {"calories": "228", "ingredients": [{"step": "1 (7 ounce) can white tuna, drained and flaked"}, {"step": "6 tablespoons mayonnaise or salad dressing"}, {"step": "1 tablespoon Parmesan cheese"}, {"step": "3 tablespoons sweet pickle relish"}, {"step": "1/8 teaspoon dried minced onion flakes"}, {"step": "1/4 teaspoon curry powder"}, {"step": "1 tablespoon dried parsley"}, {"step": "1 teaspoon dried dill weed"}, {"step": "1 pinch garlic powder"}], "submitter": "TANAQUIL", "description": "This is a really great tuna salad recipe I got from a friend who used it in her catering service business many years ago. The secret ingredients are the curry and Parmesan cheese! Odd combinations but this makes a terrific tuna sandwich! She used it for an appetizer with gourmet crackers and people always wanted her recipe. I have never tasted another tuna salad quite like this one, and it has been my favorite recipe for tuna salad for many, many years.", "title": "Barbie's Tuna Salad"}, {"calories": "426", "ingredients": [{"step": "1 head leaf lettuce, torn into bite-size pieces"}, {"step": "3 pears - peeled, cored and chopped"}, {"step": "5 ounces Roquefort cheese, crumbled"}, {"step": "1 avocado - peeled, pitted, and diced"}, {"step": "1/2 cup thinly sliced green onions"}, {"step": "1/4 cup white sugar"}, {"step": "1/2 cup pecans"}, {"step": "1/3 cup olive oil"}, {"step": "3 tablespoons red wine vinegar"}, {"step": "1 1/2 teaspoons white sugar"}, {"step": "1 1/2 teaspoons prepared mustard"}, {"step": "1 clove garlic, chopped"}, {"step": "1/2 teaspoon salt"}, {"step": "fresh ground black pepper to taste"}], "submitter": "Michelle Krzmarzick", "description": "This is the best salad I've ever eaten and I make it all the time. It is tangy from the blue cheese, fruity from the pears, and crunchy from the caramelized pecans. The mustard vinaigrette pulls it all together.", "title": "Roquefort Pear Salad"}, {"calories": "391", "ingredients": [{"step": "1/3 cup fresh lime juice"}, {"step": "1/2 cup olive oil"}, {"step": "1 clove garlic, minced"}, {"step": "1 teaspoon salt"}, {"step": "1/8 teaspoon ground cayenne pepper"}, {"step": "2 (15 ounce) cans black beans, rinsed and drained"}, {"step": "1 1/2 cups frozen corn kernels"}, {"step": "1 avocado - peeled, pitted and diced"}, {"step": "1 red bell pepper, chopped"}, {"step": "2 tomatoes, chopped"}, {"step": "6 green onions, thinly sliced"}, {"step": "1/2 cup chopped fresh cilantro (optional)"}], "submitter": "Jen", "description": "This salad is very colorful and includes a very tasty lime dressing.", "title": "Black Bean and Corn Salad II"}, {"calories": "235", "ingredients": [{"step": "2 bunches spinach, rinsed and torn into bite-size pieces"}, {"step": "4 cups sliced strawberries"}, {"step": "1/2 cup vegetable oil"}, {"step": "1/4 cup white wine vinegar"}, {"step": "1/2 cup white sugar"}, {"step": "1/4 teaspoon paprika"}, {"step": "2 tablespoons sesame seeds"}, {"step": "1 tablespoon poppy seeds"}], "submitter": "JerJer", "description": "My family loves this all year round if we can find strawberries. Even the grandchildren love this salad. Quick and easy.", "title": "Spinach and Strawberry Salad"}, {"calories": "384", "ingredients": [{"step": "6 cloves garlic, peeled, divided"}, {"step": "3/4 cup mayonnaise"}, {"step": "5 anchovy fillets, minced"}, {"step": "6 tablespoons grated Parmesan cheese, divided"}, {"step": "1 teaspoon Worcestershire sauce"}, {"step": "1 teaspoon Dijon mustard"}, {"step": "1 tablespoon lemon juice, or more to taste"}, {"step": "salt to taste"}, {"step": "ground black pepper to taste"}, {"step": "1/4 cup olive oil"}, {"step": "4 cups day-old bread, cubed"}, {"step": "1 head romaine lettuce, torn into bite-size pieces"}], "submitter": "Karen  Weir", "description": "A wonderful, rich, anchovy dressing makes this salad a meal. Serve with crusty Italian Bread.", "title": "Caesar Salad Supreme"}, {"calories": "315", "ingredients": [{"step": "4 cups cubed, cooked chicken meat"}, {"step": "1 cup mayonnaise"}, {"step": "1 teaspoon paprika"}, {"step": "1 1/2 cups dried cranberries"}, {"step": "1 cup chopped celery"}, {"step": "2 green onions, chopped"}, {"step": "1/2 cup minced green bell pepper"}, {"step": "1 cup chopped pecans"}, {"step": "1 teaspoon seasoning salt"}, {"step": "ground black pepper to taste"}], "submitter": "emmaxwell", "description": "Serve on lettuce cups, or make sandwiches.  Stand back and enjoy the applause!", "title": "Holiday Chicken Salad"}, {"calories": "273", "ingredients": [{"step": "8 slices bacon"}, {"step": "2 heads fresh broccoli, chopped"}, {"step": "1 1/2 cups sharp Cheddar cheese, shredded"}, {"step": "1/2 large red onion, chopped"}, {"step": "1/4 cup red wine vinegar"}, {"step": "1/8 cup white sugar"}, {"step": "2 teaspoons ground black pepper"}, {"step": "1 teaspoon salt"}, {"step": "2/3 cup mayonnaise"}, {"step": "1 teaspoon fresh lemon juice"}], "submitter": "Cassandra Kennedy", "description": "This recipe is requested at every family gathering. Let it be your next dish that they crave! I like this dish to be prepared at least two hours before serving. Be sure to have copies of the recipe on hand, as everyone will ask for it!", "title": "Bodacious Broccoli Salad"}, {"calories": "344", "ingredients": [{"step": "8 eggs"}, {"step": "1/2 cup mayonnaise"}, {"step": "1 teaspoon prepared yellow mustard"}, {"step": "1/4 cup chopped green onion"}, {"step": "salt and pepper to taste"}, {"step": "1/4 teaspoon paprika"}], "submitter": "wifeyluvs2cook", "description": "This is a wonderful-tasting egg salad sandwich that you will definitely devour. It's really good on rye.", "title": "Delicious Egg Salad for Sandwiches"}, {"calories": "451", "ingredients": [{"step": "1 pound seashell pasta"}, {"step": "1/4 pound Genoa salami, chopped"}, {"step": "1/4 pound pepperoni sausage, chopped"}, {"step": "1/2 pound Asiago cheese, diced"}, {"step": "1 (6 ounce) can black olives, drained and chopped"}, {"step": "1 red bell pepper, diced"}, {"step": "1 green bell pepper, chopped"}, {"step": "3 tomatoes, chopped"}, {"step": "1 (.7 ounce) package dry Italian-style salad dressing mix"}, {"step": "3/4 cup extra virgin olive oil"}, {"step": "1/4 cup balsamic vinegar"}, {"step": "2 tablespoons dried oregano"}, {"step": "1 tablespoon dried parsley"}, {"step": "1 tablespoon grated Parmesan cheese"}, {"step": "salt and ground black pepper to taste"}], "submitter": "Dayna", "description": "A delicious pasta, meat and cheese combination with a homemade dressing. It serves a crowd and is great for a picnic.", "title": "Antipasto Pasta Salad"}, {"calories": "277", "ingredients": [{"step": "1/2 cup white sugar"}, {"step": "1/2 cup lemon juice"}, {"step": "2 teaspoons diced onion"}, {"step": "1 teaspoon Dijon-style prepared mustard"}, {"step": "1/2 teaspoon salt"}, {"step": "2/3 cup vegetable oil"}, {"step": "1 tablespoon poppy seeds"}, {"step": "1 head romaine lettuce, torn into bite-size pieces"}, {"step": "4 ounces shredded Swiss cheese"}, {"step": "1 cup cashews"}, {"step": "1/4 cup dried cranberries"}, {"step": "1 apple - peeled, cored and diced"}, {"step": "1 pear - peeled, cored and sliced"}], "submitter": "Nora LaCroix", "description": "Wonderful salad for the holiday seasons. Great to serve for dinner at home or to take to a family gathering during the holidays.", "title": "Winter Fruit Salad with Lemon Poppyseed Dressing"}, {"calories": "336", "ingredients": [{"step": "1 (12 ounce) package uncooked tri-color rotini pasta"}, {"step": "10 slices bacon"}, {"step": "1 cup mayonnaise"}, {"step": "3 tablespoons dry ranch salad dressing mix"}, {"step": "1/4 teaspoon garlic powder"}, {"step": "1/2 teaspoon garlic pepper"}, {"step": "1/2 cup milk, or as needed"}, {"step": "1 large tomato, chopped"}, {"step": "1 (4.25 ounce) can sliced black olives"}, {"step": "1 cup shredded sharp Cheddar cheese"}], "submitter": "Wilemon", "description": "This is a very flavorful pasta salad. The crisp cooked bacon really adds a nice flavor. I get requests for this pasta salad for every get together and cook out.", "title": "Bacon Ranch Pasta Salad"}, {"calories": "253", "ingredients": [{"step": "1 cup uncooked couscous"}, {"step": "1 1/4 cups chicken broth"}, {"step": "3 tablespoons extra virgin olive oil"}, {"step": "2 tablespoons fresh lime juice"}, {"step": "1 teaspoon red wine vinegar"}, {"step": "1/2 teaspoon ground cumin"}, {"step": "8 green onions, chopped"}, {"step": "1 red bell pepper, seeded and chopped"}, {"step": "1/4 cup chopped fresh cilantro"}, {"step": "1 cup frozen corn kernels, thawed"}, {"step": "2 (15 ounce) cans black beans, drained"}, {"step": "salt and pepper to taste"}], "submitter": "Paula", "description": "This is a great salad for a buffet, with interesting textures and southwest flavors combined in one delicious salad.  Leftovers store well refrigerated for several days.", "title": "Black Bean and Couscous Salad"}, {"calories": "374", "ingredients": [{"step": "2 heads fresh broccoli"}, {"step": "1 red onion"}, {"step": "1/2 pound bacon"}, {"step": "3/4 cup raisins"}, {"step": "3/4 cup sliced almonds"}, {"step": "1 cup mayonnaise"}, {"step": "1/2 cup white sugar"}, {"step": "2 tablespoons white wine vinegar"}], "submitter": "Nora", "description": "This is a yummy summer salad that uses an interesting combination of fruits, vegetables and meats.  Before you decide you won't like it, try it.  You'll be pleasantly surprised.  You can add an extra head of broccoli, if you like.", "title": "Fresh Broccoli Salad"}]
```

</details>

<details><summary>21. Flask + Hive + Hadoop</summary>

```bash
compose/bash
python3 app.py
curl http://localhost:5000/employee/Gopal/
```

```text
[[1201, "Gopal", "45000", "Technical manager"]]
```

</details>
