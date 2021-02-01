``` java
import java.util.*;
import java.io.*;

class Main {
    public static void main(String[] args) throws IOException {
        StringTokenizer st;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        ArrayList<Student> list = new ArrayList<>();

        int N = Integer.parseInt(br.readLine());
        for (int i = 0; i < N; i++) {
            st = new StringTokenizer(br.readLine(), " ");

            String name = st.nextToken();
            int korean = Integer.parseInt(st.nextToken());
            int english = Integer.parseInt(st.nextToken());
            int math = Integer.parseInt(st.nextToken());

            list.add(new Student(name, korean, english, math));
        }

        Collections.sort(list);

        for (Student student : list) {
            bw.write(student.name + "\n");
        }
        bw.flush();

        br.close();
        bw.close();
    }

    static class Student implements Comparable<Student>{
        String name;
        int korean, english, math;

        Student(String name, int korean, int english, int math) {
            this.name = name;
            this.korean = korean;
            this.english = english;
            this.math = math;
        }

        @Override
        public int compareTo(Student o) {
            int result;

            if (korean > o.korean) {
                result = -1;
            } else if (korean < o.korean) {
                result = 1;
            } else if (english > o.english) {
                result = 1;
            } else if (english < o.english) {
                result = -1;
            } else if (math > o.math) {
                result = -1;
            } else if (math < o.math) {
                result = 1;
            } else {
                result = name.compareTo(o.name);
            }

            return result;
        }
    }
}
```
