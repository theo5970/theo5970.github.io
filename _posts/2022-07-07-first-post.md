---
title: 안녕하세요
date: 2022-07-07 05:34:30 +0900
categories: [Notice]
---

제가 첫 기술 블로그를 시작하게 되었습니다.

여기에는 유니티, C# 등등 강좌를 연재할 예정입니다.

잘 부탁드려요~

- - -
아래는 테스트 코드 스니펫입니다.

```cs
using Newtonsoft.Json;

public class NoteEvent : GameEvent
{
    [JsonIgnore]
    public float StartPos => startPos;
    private float startPos;

    [JsonIgnore]
    public float EndPos => endPos;
    private float endPos;

    public NoteEvent() : base() { }
    public NoteEvent(float startBeat) : base(startBeat) { }
    public NoteEvent(float startBeat, float endBeat) : base(startBeat, endBeat) { }

    public void AcceptPositionCalculator(INotePositionCalculator calculator)
    {
        startPos = calculator.TimeToPos(Time);
        if (IsLong)
        {
            endPos = calculator.TimeToPos(EndTime);
        }
    }
}

```

```rs
fn main() {
    let str1 = String::from("Hello, World!")
    println!(str1);
}
```