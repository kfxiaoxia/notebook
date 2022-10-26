```Swift
    @objc func rollingAnimation() {

        let ts = CATransition()

        ts.type = .push

        ts.subtype = .fromTop

        self.rollingLabel.layer.add(ts, forKey: "trans")

        self.rollingLabel.text = arr[currentIndex]

        if currentIndex == self.arr.count - 1 {

            currentIndex = 0

        } else {

            currentIndex += 1

        }

    }
```