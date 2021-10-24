# Favourite Genres

Given a map Map<String, List<String>> userSongs with user names as keys and a list of all the songs that the user has listened to as values.

Also given a map Map<String, List<String>> songGenres, with song genre as keys and a list of all the songs within that genre as values. The song can only belong to only one genre.

The task is to return a map Map<String, List<String>>, where the key is a user name and the value is a list of the user's favorite genre(s). Favorite genre is the most listened to genre. A user can have more than one favorite genre if he/she has listened to the same number of songs per each of the genres.
```
Example 1:

Input:
userSongs = {  
   "David": ["song1", "song2", "song3", "song4", "song8"],
   "Emma":  ["song5", "song6", "song7"]
},
songGenres = {  
   "Rock":    ["song1", "song3"],
   "Dubstep": ["song7"],
   "Techno":  ["song2", "song4"],
   "Pop":     ["song5", "song6"],
   "Jazz":    ["song8", "song9"]
}

Output: {  
   "David": ["Rock", "Techno"],
   "Emma":  ["Pop"]
}

Explanation:
David has 2 Rock, 2 Techno and 1 Jazz song. So he has 2 favorite genres.
Emma has 2 Pop and 1 Dubstep song. Pop is Emma's favorite genre.
```
```
Example 2:

Input:
userSongs = {  
   "David": ["song1", "song2"],
   "Emma":  ["song3", "song4"]
},
songGenres = {}

Output: {  
   "David": [],
   "Emma":  []
}
```
	
## Implementation :	

```java
import java.util.*;

public class App {

	public static void main(String[] args) {
		Map<String, List<String>> userSongs = new HashMap<>();
		List<String> davidList = new ArrayList<>();
		davidList.add("song1"); davidList.add("song2"); davidList.add("song3"); davidList.add("song4"); davidList.add("song8");
		userSongs.put("David", davidList);
		List<String> emmaList = new ArrayList<>();
		emmaList.add("song5");emmaList.add("song6"); emmaList.add("song7");
		userSongs.put("Emma", emmaList);
		
		Map<String, List<String>> genreMap = new HashMap<>();
		List<String> rock = new ArrayList<>();
		rock.add("song1"); rock.add("song3");
		List<String> dubstep = new ArrayList<>();
		dubstep.add("song7");
		List<String> techno = new ArrayList<>();
		techno.add("song2"); techno.add("song4");
		List<String> pop = new ArrayList<>();
		pop.add("song5"); pop.add("song6");
		List<String> jazz = new ArrayList<>();
		jazz.add("song8"); jazz.add("song9");
		genreMap.put("Rock", rock);
		genreMap.put("Dubstep", dubstep);
		genreMap.put("Techno", techno);
		genreMap.put("Pop", pop);
		genreMap.put("Jazz", jazz);
		System.out.println(new App().favouriteGenres(userSongs, genreMap));

	}
	
	private Map<String,List<String>> favouriteGenres(Map<String, List<String>> userSongs, Map<String, List<String>> genreMap) {
		Map<String, List<String>> output = new HashMap<>();
		
		// first lets create a map for song => genre, this map will help us find the genre of a song
		Map<String,String> songGenreMap = new HashMap<>();
		for(String genre : genreMap.keySet()) {
			for(String song : genreMap.get(genre)) {
				songGenreMap.put(song, genre);	
			}
		}
		
		for(String user : userSongs.keySet()) {
			// lets create a map to track the count of genre that user have listen
			// also we will track the max number (most listen genre count)
			Map<String, Integer> genreCount = new HashMap<>();
			int max = 0;
			for(String song : userSongs.get(user)) {
				String genre = songGenreMap.get(song);
				if(genre != null) {
					int count = genreCount.getOrDefault(genre, 0);
					genreCount.put(genre, count + 1);
					max = Math.max(max, count + 1);
				}
			}

			output.put(user, new ArrayList<String>());
			
			// now lets add the favourite genre of the user to the output
			for(String genre : genreCount.keySet()) {
				if(genreCount.get(genre) == max) {
					output.get(user).add(genre);
				}
			}
		}
		return output;
	}

}

```

