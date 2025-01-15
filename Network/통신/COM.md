# COM(Component Object Model)

## COM이란?

+   COM(Component Object Model)은 Microsoft에서 개발한 소프트웨어 구성 요소 기술로, 소프트웨어 간의 상호작용과 재사용성을 높이기 위해 설계되었습니다.

+   다양한 프로그래밍 언어와 환경에서 객체 지향적인 방식으로 컴포넌트를 정의하고 사용할 수 있게 해줍니다.

+   window 환경에서 애플리케이션 간의 상호작용을 지원하기 위해 널리 사용됩니다.

## COM의 장단점

+   장점
    -   소프트웨어 재사용성 증대
    -   언어 독립성
    -   프로세스 간 통신 지원
    -   유지보수 및 확장성 용이

+   단점
    -   복잡한 개발 및 디버깅
    -   레지스트리 의존성으로 인한 배포 어려움
    -   참조 카운팅 오류로 인한 메모리 누수 가능성

## 알게된 점

+   통신 환경에 따라 데이터 송수신 품질이 저하될 가능성이 높다.
+   통신 매체에 따라 데이터 송수신 품질이 달라질 수 있다.
+   통신 환경과 통신 매개체에 적합한 방식을 찾아야 한다.

### 문제상황
+   com 통신시 송신한 데이터가 손실되거나 정상적으로 출력되지 않는 현상.
    ## 해결방안
        1.1 부분 데이터 수신 처리
        -   수신된 데이터를 바이트 버퍼(buffer)에 누적하여 데이터가 완전할 때까지 대기.
        -   줄바꿈 문자(\n)를 기준으로 데이터를 처리하고, 미완성 데이터는 버퍼에 보존.
        1.2 데이터 타입 일관성 유지
        -   수신된 데이터는 항상 바이트 타입(bytes)로 처리.
        -   데이터 디코딩은 UTF-8로 명시적으로 수행.
        1.3 미완성 데이터 보존
        -   줄바꿈 문자가 없는 미완성 데이터는 buffer에 유지하여 다음 수신 데이터와 결합 후 처리.
        1.4 송신 데이터 인코딩 확인
        -   송신 측에서 데이터를 반드시 UTF-8로 인코딩 후 전송하도록 수정.
    
    ## com 송신 코드 (python)
        import serial
        import time

        def send_data():
            # COM 포트 번호 및 설정 (예: COM1, COM2)
            port = "COM10"
            baudrate = 9600
            
            # 직렬 포트 열기
            ser = serial.Serial(port, baudrate)
            
            choice = input("데이터 보내는 방식 선택(1: 자동, 0: 수동): ")
            
            # 데이터 송신
            if choice == '0':
                while True:
                    data = input("")  # 전송할 데이터
                    data_write = f"{data}\n" 
                    ser.write(data_write.encode('utf-8'))  # 데이터 전송
                    print(f"Sent: {data_write}")

            elif choice == '1':
                while True:
                    data = "안녕하세요 \n"  # 전송할 데이터 \n은 데이터의 끝을 의미
                    ser.write(data.encode('utf-8'))  # 데이터 전송
                    print(f"Sent: {data}")
                    time.sleep(1)  # n초 대기 후 반복 송신

        if __name__ == "__main__":
            send_data()

    ## com 수신 코드 (python)
        import serial

        def receive_data():
            # COM 포트 번호 및 설정
            port = "COM11"
            baudrate = 9600

            # 직렬 포트 열기
            ser = serial.Serial(port, baudrate, timeout=1)
            
            buffer = b""  # 수신된 데이터 저장용 버퍼

            while True:
                if ser.in_waiting > 0:  # 데이터가 도착한 경우
                    data = ser.read(ser.in_waiting)
                    buffer += data # 누적
                    
                    if b"\n" in buffer:  # '\n'이 있는 경우      바이트 리터럴로 검사
                        line, buffer = buffer.split(b"\n", 1)
                        print(f"Received: {line.decode('utf-8', errors='replace').strip()}")  # 수신한 데이터 출력

        if __name__ == "__main__":
            receive_data()


    ## 주요 오류 메시지
        raise SerialException("could not open port {!r}: {!r}".format(self.portstr, ctypes.WinError()))     
        serial.serialutil.SerialException: could not open port 'COM5': PermissionError(13, '액세스가 거부되었습니다.', None, 5)

    +   com5 포트를 이미 사용하고 있다는 메시지입니다. com5 사용을 중단하고 다시 실행하면 해결 됩니다.


    ## 실습
        VSPD를 사용하면 가상의 Com포트를 생성해서 데이터 송수신을 할 수 있습니다.
        