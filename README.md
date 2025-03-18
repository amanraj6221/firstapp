import React, { useEffect, useState } from 'react';

const ProductDetails = () => {
  const [products, setProducts] = useState([]); 
  useEffect(() => {
   
    fetch('https://fakestoreapi.com/products?limit=10')
    .then(response => response.json())
     .then(data => setProducts(data));
    }, [])

  return (
    <div className="container mt-5">
      <div className="row d-flex justify-content-start">
        {products.map((product, index) => (
          <div key={index} className="col-md-4 mb-4">
            <div className="card" style={{ width: '100%' }}>
              <img src={product.image} className="card-img-top" alt={product.title} />
              <div className="card-body">
                <h5 className="card-title">{product.title}</h5>
                {/* <p className="card-text">{product.description}</p> */}
                <p className="card-text">Price: ${product.price}</p>
                <p className="card-text">Category: {product.category}</p>
                <p className="card-text">Rating: {product.rating.rate} (Rated {product.rating.count} times)</p>
              </div>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
}

export default ProductDetails;
