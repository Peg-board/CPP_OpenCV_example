# 제목 없음

$$
\huge {\textsf {C++에서 OpenCV 활용하기}}
$$

```
환경
OS: macOS Sonoma
IDE: XCODE version 15.3 (15E204a), Visual Studio Code version 1.89.0

```

# **`SUBSCRIPTION`**

## Homebrew 설치

Homebrew는 macOS용 패키지 관리 애플리케이션이다. 설치, 업데이트, 삭제 등 관리가 용이하다.

```
[https://brew.sh/](https://brew.sh/)
```

(1) sudo 권한을 인증하고 설치한다. (install with curl)

```bash
// 설치
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

(2) `Press **RETURN/ENTER** to continue or any other key to abort`라고 표기 되면 엔터로 계속진행

![스크린샷 2024-01-30 오후 8.47.56.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-01-30_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_8.47.56.png?raw=true)

(3) 설치가 완료 후 다음단계인 명령어 실행

![스크린샷 2024-01-30 오후 8.51.38.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-01-30_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_8.51.38.png?raw=true)

```c
/** 'eval "$(/usr/local/bin/brew shellenv)"'를 /Users/사용자 이름/.zprofile 에 추가한다.*/
(echo; echo 'eval "$(/usr/local/bin/brew shellenv)"') >> /Users/username/.zprofile

/** zsh쉘이 시작할 때 brew도 함께 실행하게 하는 초기화 스크립트*/
eval "$(/usr/local/bin/brew shellenv)"
```

(4)확인

```c
brew --version // 테스트
```

## OpenCV 설치

```bash
brew install opencv
```

# **`Xcode`**

## 프로젝트 생성

(1) `Create a new Xcode project` 클릭

![스크린샷 2024-05-08 오후 9.01.45.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_9.01.45.png)

(2) macOS → Command Line Tool 선택 → Next 클릭

![스크린샷 2024-05-08 오후 9.02.03.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_9.02.03.png)

(3) 프로젝트 이름, 조직 식별자, 언어 입력 → Next 클릭

![스크린샷 2024-05-08 오후 9.02.42.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_9.02.42.png)

## 동적 라이브러리 불러오기

(1) 프로젝트 우클릭→ Add Files to “프로젝트 이름”

![스크린샷 2024-05-08 오후 10.21.19.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_10.21.19.png)

(2) OpenCV 동적 라이브러리 가 있는 패키지 경로로 이동(Go to Folder: command(⌘) + shift(⇧) + g)

```
/usr/local/Cellar/opencv
```

![스크린샷 2024-05-08 오후 10.21.40.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_10.21.40.png)

(3)[OpenCV 버전] → lib → .dylib(유형: `Unix Executable File` ) 모두 선택

(정렬기준을 “Kind”로 설정시 선택이 용이함 )

![스크린샷 2024-05-08 오후 10.23.10.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_10.23.10.png)

![스크린샷 2024-05-08 오후 10.31.49.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_10.31.49.png)

## 해더 패스(Header Path) 설정

패키지의 경로를 제시하여 해더 파일을 빠르게 가져올 수 있다.

(1)프로젝트 → Build Settings → `All`, `Combind` 선택 → `Header Search Paths` 검색

![스크린샷 2024-05-08 오후 11.18.34.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_11.18.34.png)

(2) opencv4의 절대 경로 입력(하위 폴더에 접근할 수 있게 `recursive`로 설정)

```
// 버전은 상이할 수 있음
/usr/local/Cellar/opencv/4.9.0_8/include/opencv4
```

![스크린샷 2024-05-08 오후 11.22.33.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_11.22.33.png)

![스크린샷 2024-05-08 오후 11.25.13.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_11.25.13.png)

## 작업 폴더(Working Directory) 설정

파일의 입출력을 위해 작업 폴더 설정

(1)메뉴막대 → Product → Scheme → Edit Scheme

![스크린샷 2024-05-08 오후 11.31.15.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_11.31.15.png)

(2) Run → Options → Working Directory 클릭 → 프로젝트 경로 입력

![스크린샷 2024-05-08 오후 11.35.45.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_11.35.45.png)

## 인자 설정

프로그램 실행 시 입력되는 인자를 설정할 수 있다.

(1)메뉴막대 → Product → Scheme → Edit Scheme

![스크린샷 2024-05-08 오후 11.31.15.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_11.31.15.png)

(2) Run → Arguments → Arguments Passed On Launch → 파일 설정

![스크린샷 2024-05-08 오후 11.48.21.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-08_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_11.48.21.png)

## 코드-1

```cpp
// edge.cpp

#include "opencv2/core/utility.hpp"
#include "opencv2/imgproc.hpp"
#include "opencv2/imgcodecs.hpp"
#include "opencv2/highgui.hpp"

#include <stdio.h>

using namespace cv;
using namespace std;

int edgeThresh = 1;
int edgeThreshScharr=1;

Mat image, gray, blurImage, edge1, edge2, cedge;

const char* window_name1 = "Edge map : Canny default (Sobel gradient)";
const char* window_name2 = "Edge map : Canny with custom gradient (Scharr)";

// define a trackbar callback
static void onTrackbar(int, void*)
{
    blur(gray, blurImage, Size(3,3));

    // Run the edge detector on grayscale
    Canny(blurImage, edge1, edgeThresh, edgeThresh*3, 3);
    cedge = Scalar::all(0);

    image.copyTo(cedge, edge1);
    imshow(window_name1, cedge);

    /// Canny detector with scharr
    Mat dx,dy;
    Scharr(blurImage,dx,CV_16S,1,0);
    Scharr(blurImage,dy,CV_16S,0,1);
    Canny( dx,dy, edge2, edgeThreshScharr, edgeThreshScharr*3 );
    /// Using Canny's output as a mask, we display our result
    cedge = Scalar::all(0);
    image.copyTo(cedge, edge2);
    imshow(window_name2, cedge);
}

static void help(const char** argv)
{
    printf("\nThis sample demonstrates Canny edge detection\n"
           "Call:\n"
           "    %s [image_name -- Default is fruits.jpg]\n\n", argv[0]);
}

const char* keys =
{
    "{help h||}{@image |fruits.jpg|input image name}"
};

int main( int argc, const char** argv )
{
    help(argv);
    CommandLineParser parser(argc, argv, keys);
    string filename = parser.get<string>(0);

    image = imread(samples::findFile(filename), IMREAD_COLOR);
    if(image.empty())
    {
        printf("Cannot read image file: %s\n", filename.c_str());
        help(argv);
        return -1;
    }
    cedge.create(image.size(), image.type());
    cvtColor(image, gray, COLOR_BGR2GRAY);

    // Create a window
    namedWindow(window_name1, 1);
    namedWindow(window_name2, 1);

    // create a toolbar
    createTrackbar("Canny threshold default", window_name1, &edgeThresh, 100, onTrackbar);
    createTrackbar("Canny threshold Scharr", window_name2, &edgeThreshScharr, 400, onTrackbar);

    // Show the image
    onTrackbar(0, 0);

    // Wait for a key stroke; the same function arranges events processing
    waitKey(0);

    return 0;
}

```

```cpp
// drawing.cpp

#include "opencv2/core.hpp"
#include "opencv2/imgproc.hpp"
#include "opencv2/highgui.hpp"
#include <stdio.h>

using namespace cv;

static void help(char** argv)
{
    printf("\nThis program demonstrates OpenCV drawing and text output functions.\n"
    "Usage:\n"
    "   %s\n", argv[0]);
}
static Scalar randomColor(RNG& rng)
{
    int icolor = (unsigned)rng;
    return Scalar(icolor&255, (icolor>>8)&255, (icolor>>16)&255);
}

int main(int /* argc */, char** argv)
{
    help(argv);
    char wndname[] = "Drawing Demo";
    const int NUMBER = 100;
    const int DELAY = 5;
    int lineType = LINE_AA; // change it to LINE_8 to see non-antialiased graphics
    int i, width = 1000, height = 700;
    int x1 = -width/2, x2 = width*3/2, y1 = -height/2, y2 = height*3/2;
    RNG rng(0xFFFFFFFF);

    Mat image = Mat::zeros(height, width, CV_8UC3);
    imshow(wndname, image);
    waitKey(DELAY);

    for (i = 0; i < NUMBER * 2; i++)
    {
        Point pt1, pt2;
        pt1.x = rng.uniform(x1, x2);
        pt1.y = rng.uniform(y1, y2);
        pt2.x = rng.uniform(x1, x2);
        pt2.y = rng.uniform(y1, y2);

        int arrowed = rng.uniform(0, 6);

        if( arrowed < 3 )
            line( image, pt1, pt2, randomColor(rng), rng.uniform(1,10), lineType );
        else
            arrowedLine(image, pt1, pt2, randomColor(rng), rng.uniform(1, 10), lineType);

        imshow(wndname, image);
        if(waitKey(DELAY) >= 0)
            return 0;
    }

    for (i = 0; i < NUMBER * 2; i++)
    {
        Point pt1, pt2;
        pt1.x = rng.uniform(x1, x2);
        pt1.y = rng.uniform(y1, y2);
        pt2.x = rng.uniform(x1, x2);
        pt2.y = rng.uniform(y1, y2);
        int thickness = rng.uniform(-3, 10);
        int marker = rng.uniform(0, 10);
        int marker_size = rng.uniform(30, 80);

        if (marker > 5)
            rectangle(image, pt1, pt2, randomColor(rng), MAX(thickness, -1), lineType);
        else
            drawMarker(image, pt1, randomColor(rng), marker, marker_size );

        imshow(wndname, image);
        if(waitKey(DELAY) >= 0)
            return 0;
    }

    for (i = 0; i < NUMBER; i++)
    {
        Point center;
        center.x = rng.uniform(x1, x2);
        center.y = rng.uniform(y1, y2);
        Size axes;
        axes.width = rng.uniform(0, 200);
        axes.height = rng.uniform(0, 200);
        double angle = rng.uniform(0, 180);

        ellipse( image, center, axes, angle, angle - 100, angle + 200,
                 randomColor(rng), rng.uniform(-1,9), lineType );

        imshow(wndname, image);
        if(waitKey(DELAY) >= 0)
            return 0;
    }

    for (i = 0; i< NUMBER; i++)
    {
        Point pt[2][3];
        pt[0][0].x = rng.uniform(x1, x2);
        pt[0][0].y = rng.uniform(y1, y2);
        pt[0][1].x = rng.uniform(x1, x2);
        pt[0][1].y = rng.uniform(y1, y2);
        pt[0][2].x = rng.uniform(x1, x2);
        pt[0][2].y = rng.uniform(y1, y2);
        pt[1][0].x = rng.uniform(x1, x2);
        pt[1][0].y = rng.uniform(y1, y2);
        pt[1][1].x = rng.uniform(x1, x2);
        pt[1][1].y = rng.uniform(y1, y2);
        pt[1][2].x = rng.uniform(x1, x2);
        pt[1][2].y = rng.uniform(y1, y2);
        const Point* ppt[2] = {pt[0], pt[1]};
        int npt[] = {3, 3};

        polylines(image, ppt, npt, 2, true, randomColor(rng), rng.uniform(1,10), lineType);

        imshow(wndname, image);
        if(waitKey(DELAY) >= 0)
            return 0;
    }

    for (i = 0; i< NUMBER; i++)
    {
        Point pt[2][3];
        pt[0][0].x = rng.uniform(x1, x2);
        pt[0][0].y = rng.uniform(y1, y2);
        pt[0][1].x = rng.uniform(x1, x2);
        pt[0][1].y = rng.uniform(y1, y2);
        pt[0][2].x = rng.uniform(x1, x2);
        pt[0][2].y = rng.uniform(y1, y2);
        pt[1][0].x = rng.uniform(x1, x2);
        pt[1][0].y = rng.uniform(y1, y2);
        pt[1][1].x = rng.uniform(x1, x2);
        pt[1][1].y = rng.uniform(y1, y2);
        pt[1][2].x = rng.uniform(x1, x2);
        pt[1][2].y = rng.uniform(y1, y2);
        const Point* ppt[2] = {pt[0], pt[1]};
        int npt[] = {3, 3};

        fillPoly(image, ppt, npt, 2, randomColor(rng), lineType);

        imshow(wndname, image);
        if(waitKey(DELAY) >= 0)
            return 0;
    }

    for (i = 0; i < NUMBER; i++)
    {
        Point center;
        center.x = rng.uniform(x1, x2);
        center.y = rng.uniform(y1, y2);

        circle(image, center, rng.uniform(0, 300), randomColor(rng),
               rng.uniform(-1, 9), lineType);

        imshow(wndname, image);
        if(waitKey(DELAY) >= 0)
            return 0;
    }

    for (i = 1; i < NUMBER; i++)
    {
        Point org;
        org.x = rng.uniform(x1, x2);
        org.y = rng.uniform(y1, y2);

        putText(image, "Testing text rendering", org, rng.uniform(0,8),
                rng.uniform(0,100)*0.05+0.1, randomColor(rng), rng.uniform(1, 10), lineType);

        imshow(wndname, image);
        if(waitKey(DELAY) >= 0)
            return 0;
    }

    Size textsize = getTextSize("OpenCV forever!", FONT_HERSHEY_COMPLEX, 3, 5, 0);
    Point org((width - textsize.width)/2, (height - textsize.height)/2);

    Mat image2;
    for( i = 0; i < 255; i += 2 )
    {
        image2 = image - Scalar::all(i);
        putText(image2, "OpenCV forever!", org, FONT_HERSHEY_COMPLEX, 3,
                Scalar(i, i, 255), 5, lineType);

        imshow(wndname, image2);
        if(waitKey(DELAY) >= 0)
            return 0;
    }

    waitKey();
    return 0;
}

```

## 결과

| 입력 영상 | 테스트 영상 |
| --- | --- |
|  |  |

![sample.jpg](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/sample.jpg)

![스크린샷 2024-05-09 오전 12.00.30.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-09_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%258C%25E1%2585%25A5%25E1%2586%25AB_12.00.30.png)

![스크린샷 2024-05-09 오전 12.11.49.png](https://github.com/Peg-board/CPP_OpenCV_example/blob/master/images/md/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-05-09_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%258C%25E1%2585%25A5%25E1%2586%25AB_12.11.49.png)
