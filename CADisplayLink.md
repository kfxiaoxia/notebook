``` Swift
    var displaylink: CADisplayLink?

    func startDisplayLink() {

        if self.displaylink != nil {

            self.displaylink?.invalidate()

            self.displaylink = nil

        }

        self.displaylink = CADisplayLink(target: self, selector: #selector(linkTriggered(displaylink: )))

        self.displaylink?.preferredFramesPerSecond = 10

        self.displaylink?.add(to: .main, forMode: .default)

    }

    @objc func linkTriggered(displaylink: CADisplayLink)  {

        for key in self.displayCells.keys {

            let value = self.displayCells[key]

            if let cell = value?.last {

                let maxX = cell.layer.presentation()?.frame.maxX ?? 0

                if maxX <= UIScreen.main.bounds.width * 0.8 ,  self.lanes[cell.lane!.number].status == .busy

                {

                    self.lanes[cell.lane!.number].status = .free

                }

            }

        }

  

    }
```