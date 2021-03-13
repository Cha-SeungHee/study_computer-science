``` java
import java.util.*;

class Solution {
    String[] noteSharp = {"C#", "D#", "F#", "G#", "A#"};
    String[] newNoteSharp = {"c", "d", "f", "g", "a"};
    
    public String solution(String m, String[] musicinfos) {
        PriorityQueue<Song> queue = new PriorityQueue<>((s1, s2) -> {
           return -(s1.duration - s2.duration);
        });
        
        for (int i = 0; i < noteSharp.length; i++) {
            m = m.replaceAll(noteSharp[i], newNoteSharp[i]);            
        }        
        
        for (String music : musicinfos) {
            StringBuilder sb = new StringBuilder();
            
            String[] musicArray = music.split(",");
            
            int duration = timeToMin(musicArray[1]) - timeToMin(musicArray[0]);
            
            for (int i = 0; i < noteSharp.length; i++) {
                musicArray[3] = musicArray[3].replaceAll(noteSharp[i], newNoteSharp[i]);
            }
            
            for (int i = 0; i < duration; i++) {
                sb.append(musicArray[3].charAt(i % musicArray[3].length()));
            }
            
            String string = sb.toString();            
            
            if (string.contains(m)) {
                queue.offer(new Song(musicArray[2], duration));
            }
        }        
        
        return (queue.isEmpty()) ? "(None)" : queue.peek().title;
    }
    
    private int timeToMin(String stringTime) {
        String[] time = stringTime.split(":");
        
        return Integer.parseInt(time[0]) * 60 + Integer.parseInt(time[1]);
    }
}

class Song {
    String title;
    int duration;
    
    Song(String title, int duration) {
        this.title = title;
        this.duration = duration;
    }
}
```

``` java
import java.util.*;

class Solution {
	
	String[] sharp = {"C#", "D#", "E#", "F#", "G#", "A#"};
	String[] lowercase = {"c", "d", "e", "f", "g", "a"};
	
	public String solution(String m, String[] musicinfos) {
		String melody = refine(m);
		String[][] infos = refine(musicinfos);
		
		Arrays.sort(infos, new Comparator<String[]>() {
			@Override
			public int compare(String[] music1, String[] music2) {
				int runningTimeOfMusic1 = Integer.parseInt(music1[0]);
				int runningTimeOfMusic2 = Integer.parseInt(music2[0]);
				
				return -(runningTimeOfMusic1 - runningTimeOfMusic2);
			}
		});
		
		for(int i = 0 ; i < infos.length ; ++i) {
			if(infos[i][2].contains(melody)) {
				return infos[i][1];
			}
		}
		
		return "(None)";
	}

	private String refine(String m) {
		String result = m;
		
		for(int i = 0 ; i < sharp.length ; ++i) {
			result = result.replaceAll(sharp[i], lowercase[i]);
		}
		
		return result;
	}
	
	private String[][] refine(String[] musicinfos) {
		String[][] infos = new String[musicinfos.length][3];
		
		for(int i = 0 ; i < musicinfos.length ; ++i) {
			String[] info = musicinfos[i].split(",");
			
			String[] start = info[0].split(":");
			String[] end = info[1].split(":");
			String title = info[2];
			String code = info[3];
			String music = "";
			
			for(int j = 0 ; j < sharp.length ; ++j) {
				code = code.replaceAll(sharp[j], lowercase[j]);
			}
			
			int musicLength = code.length();
			int runningTime = getRunningTime(start, end);
			int codeIdx = 0;
			
			for(int j = 0 ; j < runningTime ; ++j) {
				music += code.charAt(codeIdx);
				codeIdx = (codeIdx + 1) % musicLength;
			}
			
			infos[i][0] = runningTime + "";
			infos[i][1] = title;
			infos[i][2] = music;
		}
		
		return infos;
	}

	private int getRunningTime(String[] start, String[] end) {
		int runningTime = 0;
		
		int startHour = Integer.parseInt(start[0]);
		int startMinute = Integer.parseInt(start[1]);
		int endHour = Integer.parseInt(end[0]);
		int endMinute = Integer.parseInt(end[1]);
		
		runningTime = (endHour - startHour) * 60 + (endMinute - startMinute);
		
		return runningTime;
	}
}
```

- 특정 문자열이 다른 문자열이 포함되었는지 확인할 때: contains 메소드 사용  
- 반음(#포함)의 경우 replaceAll을 활용하여 소문자로 변경    
- 람다식  

``` py
import re
import sys

input = sys.stdin.readline

def calcDuration(begin, end):
    h1, m1 = begin.split(":")
    h2, m2 = end.split(":")
    
    return (int(h2) * 60 + int(m2)) - (int(h1) * 60 + int(m1)) + 1


def extractMusic(note, duration):
    result = note * (duration // len(note))
    result += note[:duration % len(note)]
    
    return result

    
def solution(m, musicinfos):
    noteMap = {'C#':'c', 'D#':'d', 'F#':'f', 'G#':'g', 'A#':'a'}
    candidate = []
    
    for i in noteMap:        
        m = m.replace(i, noteMap[i])
    
    for music in musicinfos:
        begin, end, title, note = list(music.split(","))
        
        duration = calcDuration(begin, end)
        for i in noteMap:
            note = note.replace(i, noteMap[i])
        
        piece = extractMusic(note, duration)       
        
        if m in piece:
            candidate.append(Music(duration, title)) 

    candidate.sort()
    
    return candidate[0].title if candidate else '(None)'

class Music:
    def __init__(self, duration, title):
        self.duration = duration
        self.title = title
        
    def __lt__(self, other):
        return int(self.duration) > int(other.duration)    
```
