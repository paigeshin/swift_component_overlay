# swift_component_overlay

## getOverlay()

- imageView에 특정 property를 적용하고 싶을 때 사용.

## setOverlay()

- arg1: cover하고 싶은 view
- arg2: statusbar를 가릴 것인지 아닌지 정해야한다.
- viewDidLoad() 또는 viewWillAppear()에 호출헤줘야한다

## showOverlay()

- overlay를 보여줌

## hideOverlay()

- overlay를 가려줌

```swift

//
//  Overlay.swift
//  ume
//
//  Created by shin seunghyun on 2020/07/14.
//  Copyright © 2020 haii. All rights reserved.
//

import UIKit

//UIViewController에 최적화된 Component
struct Overlay {
    
    private var imageViewOverlay: UIImageView = {
        let backgroudView: UIImageView = UIImageView()
        backgroudView.translatesAutoresizingMaskIntoConstraints = false
        backgroudView.backgroundColor = .black
        backgroudView.alpha = 0.2
        return backgroudView
    }()
    
    init() {
        
    }
    
    //유저가 UIImageView에 뭔가를 적용하고 싶을 때 사용하는 함수
    func getOverlay() -> UIImageView {
        return imageViewOverlay
    }
    
    //arg1 - overlay를 적용할 view
    //arg2 - coverStatusBar을 true로 주면 화면 전체를 cover함.
    func setOverlay(parentView: UIView, coverStatusBar: Bool) {
        parentView.addSubview(imageViewOverlay)
        parentView.sendSubviewToBack(imageViewOverlay)
        if coverStatusBar {
            imageViewOverlay.topAnchor.constraint(equalTo: parentView.topAnchor, constant: -UIApplication.shared.statusBarFrame.height).isActive = true
        } else {
            imageViewOverlay.topAnchor.constraint(equalTo: parentView.topAnchor).isActive = true
        }
        imageViewOverlay.leftAnchor.constraint(equalTo: parentView.leftAnchor).isActive = true
        imageViewOverlay.rightAnchor.constraint(equalTo: parentView.rightAnchor).isActive = true
        imageViewOverlay.bottomAnchor.constraint(equalTo: parentView.bottomAnchor).isActive = true
        imageViewOverlay.isHidden = true
    }
    
    //보여줄 때, show overlay를 호출해야한다
    func showOverlay() {
        imageViewOverlay.isHidden = false
    }
    
    //숨길 때, hide overlay를 호출해야한다.
    func hideOverlay() {
        imageViewOverlay.isHidden = true
    }
    
}




```
