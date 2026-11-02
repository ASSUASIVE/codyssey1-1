"""
스터디 출석부 프로그램 (attend.py)
- 외부 라이브러리 없이 표준 라이브러리만 사용
- 출석 기록은 attendance.csv 파일에 저장됩니다.
"""

import csv
import os
from datetime import date

# 출석 기록을 저장할 파일 이름
DATA_FILE = "attendance.csv"


def load_records():
    """저장된 출석 기록을 파일에서 읽어 리스트로 반환한다."""
    records = []
    if os.path.exists(DATA_FILE):
        with open(DATA_FILE, "r", encoding="utf-8", newline="") as f:
            reader = csv.reader(f)
            for row in reader:
                if len(row) == 2:          # [날짜, 이름] 형태만 사용
                    records.append(row)
    return records


def save_record(day, name):
    """한 건의 출석 기록을 파일 끝에 추가(append)한다."""
    with open(DATA_FILE, "a", encoding="utf-8", newline="") as f:
        writer = csv.writer(f)
        writer.writerow([day, name])


def add_attendance():
    """사용자에게 날짜와 이름을 입력받아 출석을 추가한다."""
    # 날짜를 비워두면 오늘 날짜를 자동으로 사용
    day = input("날짜 (YYYY-MM-DD, 비우면 오늘): ").strip()
    if day == "":
        day = date.today().isoformat()   # 예: 2024-05-20

    name = input("이름: ").strip()
    if name == "":
        print("⚠️ 이름은 반드시 입력해야 합니다.\n")
        return

    save_record(day, name)
    print(f"✅ 출석 완료: {day} / {name}\n")


def show_list():
    """저장된 출석 목록을 보기 좋게 출력한다."""
    records = load_records()
    if not records:
        print("아직 출석 기록이 없습니다.\n")
        return

    print("\n===== 출석 목록 =====")
    print(f"{'번호':<4}{'날짜':<14}{'이름'}")
    print("-" * 30)
    for i, (day, name) in enumerate(records, start=1):
        print(f"{i:<4}{day:<14}{name}")
    print(f"총 {len(records)}건\n")


def main():
    """메뉴를 반복해서 보여주는 프로그램의 시작점."""
    while True:
        print("===== 스터디 출석부 =====")
        print("1. 출석 추가")
        print("2. 출석 목록 보기")
        print("3. 종료")
        choice = input("선택: ").strip()

        if choice == "1":
            add_attendance()
        elif choice == "2":
            show_list()
        elif choice == "3":
            print("프로그램을 종료합니다. 수고하셨어요! 👋")
            break
        else:
            print("1, 2, 3 중에서 선택해 주세요.\n")


if __name__ == "__main__":
    main()
