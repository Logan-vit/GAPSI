# GAPSI
Proyecto búsqueda de artículos 

import UIKit

class searchViewController : UIViewController{
	
	@IBOutlet weak var searchBar: UISearchBar!
		override func viewDidLoad(){
		super.viewDidLoad()

		self.view.backgroundColor = UIColor(patternImage: UIImage(named: "https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.xataka.com.mx%2Feventos%2Fhackers-se-hacen-con-informacion-de-los-usuarios-de-liverpool&psig=AOvVaw1oskG02VveQQRtjFFvAlWt&ust=1599342310126000&source=images&cd=vfe&ved=0CAIQjRxqFwoTCMCk1d280OsCFQAAAAAdAAAAABAT"))

		title = "Ingresa el producto que deseas buscar:"

		showMenu.heightAnchor.constraint(equalToConstraint: 0).isActive = true

		showMenu.widthAnchor.constraint(equalToConstraint: 0).isActive = true

		showMenu.translatesAutoresizingMaskInToConstraints = false

		view.addConstraint(NSLayoutConstraint(item: showMenu, Attribute: .leading, relatedBy: .equal, toItem: view, attribute: .leading, Multiplier: 1000, constant: 16))

		showMenu.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor, constant: 16).isActive = true

		tableView.dataSource = self
		tableView.tableFooterView = UIView()

		myLabel.isHidden = true
		searchBar.delegate = self
	}
}


//MARK: - UITableViewDataSource

extension ViewController: UITableViewDataSource{
	
	func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int{
	}

	func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell{
		var cell = tableView.dequeueReusableCell(whitIdentifier: "mycell")

		if cell == nil{
			cell = UITableViewCell(style: .default, reuseIdentifier: "mycell")

		}
		cell.textLabel?.text = myMenu[indexPath.row]
		return cell!
	}
}

extension searchViewController: UISearchBarDelegate{
	
	func searchBarButtonClicked(_ searchBar: UISearchBar){
		searchBar.resignFirstResponder()

		myLabel.text.text = searchBar.text
		myLabel.isHidden = true
	}
}

func llamadaWebService(){
	let urlPath = "https://shoppapp.liverpool.com.mx/appclienteservices/services/v3/plp?force-plp=true&search-string=[criterio]&page-number=[x]&number-of-items-per-page=[y]"
	let url = NSUrl(String: urlPath)
	let session = NSURLSession.sharedSession()

	let task = session.dataTaskWithURL(url, completionHandler: {data, response, error -> Void in

		if error != nil{
			print(error.localizedDescription)
		}

		var nsdata:NSData = NSData(data: data)
		self.recuperar(nsdata)
	})

	var content =
	{
		"producto" : searchBar.text
		"pagina" : 
		"cantidad" :
	}

}

