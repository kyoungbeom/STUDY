# public static void main(){String args[]}
        static 멤버는 프로그램 시작시 클래스 로더에 의해 메모리에 로드되어 인스턴스를 생성하지 않아도 호출할 수 있기 때문이다.

        Rutime data area중 메서드 영역에 생성이 되기 때문에, JVM은 별도로 인스턴스를 생성하지 않아도 메서드 영역에 로드된 main()을 실행할 수 있다.
