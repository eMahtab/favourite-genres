# Favourite Genres


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
				int count = genreCount.getOrDefault(genre, 0);
				genreCount.put(genre, count + 1);
				max = Math.max(max, count + 1);
			}
			if(max != 0)
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

